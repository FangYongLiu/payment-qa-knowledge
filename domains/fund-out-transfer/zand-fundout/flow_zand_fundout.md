---
id: flow_zand_fundout
object_type: Flow
domain: fund-out-transfer
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: confluence:AQ/2049867832
tags:
- ZAND
- Fundout
- SP
- SQ
- VS
subdomain: zand-fundout
module: null
sensitivity: normal
name: ZAND渠道出款端到端流程
aliases: []
related_services: []
related_tables:
- tbl_mhtfundout_t_fundout_order
- tbl_mhtfundout_t_fundout_bankcard_order
- tbl_cmf_tt_inst_order
- tbl_cmf_tt_inst_order_result
related_scenarios:
- scn_zand_fundout_test_cases
related_logs: []
related_requirements: []
related_failures: []
---

## 概述
ZAND渠道Fundout端到端流程：从用户/商户下单 -> Fundout Service创建订单 -> Kafka异步消息 -> CMF Router路由到对应ZAND子渠道 -> SP提交支付到ZAND银行 -> （国际单）SQ轮询 -> VS回调最终状态 -> 订单标记SUCCESS/FAILED，并由DPM完成余额扣减与手续费记账。

- 国内（ZAND201/ZAND210，AED）：SP -> VS，约12秒完成，无需SQ。
- 国际（ZAND203/ZAND207，USD/SWIFT）：SP -> SQ（轮询）-> VS，异步，小时级。
- 结算流（ZAND204域内 / ZAND207国际）需要BMOC审计审批后执行。
- 商户Portal转账需要在My Authorization中授权后才进入处理。

## 步骤(跨系统)
1. 下单入口：Merchant Portal / Botim App / Partner API 发起转账或提现。
2. SGS API Gateway：完成 Auth、Validation、Rate Limiting。
3. Fundout Service：创建订单，进行 beneficiary 校验、FX 处理；写入 mhtfundout（[[tbl_mhtfundout_t_fundout_order]]、[[tbl_mhtfundout_t_fundout_bankcard_order]]、t_fundout_beneficiary）；status=CREATED/PLACED。
4. Kafka MQ：发送 fundout.created / processing / status.update 消息。
5. CMF Router：根据 partner、product_code、币种路由到 ZAND201/203/204/207/210，写入 [[tbl_cmf_tt_inst_order]]，生成 INST_ORDER_NO（如 ZAND20326031611337631），STATUS=I。
6. SP（Submit Payment）：CMF 调用 ZAND Bank SP API，银行返回 ChannelRefId（域内 D 开头，国际 ZIT 开头）；在 [[tbl_cmf_tt_inst_order_result]] 写入 API_TYPE=SP, INST_STATUS=I, INST_SEQ_NO=ChannelRefId, EXTENSION 含 CreationDateTime+ChannelRefId+channelTransTime。
   - SP 失败/超时：进入 retry handler（指数退避）-> retry queue -> worker 重提；持续失败则永久失败并冲销手续费。
7. SQ（Status Query，仅国际）：CMF 周期性轮询 ZAND；前 ~2 分钟较密，间隔逐步加大，RETRY_TIMES>35 后小时级，RETRY_TIMES=54 停止；写入 API_TYPE=SQ 行，INST_STATUS=I 或 S，ChannelRefId 与 SP 一致。
8. VS（Vendor Status Webhook）：ZAND 回调 https://uat-fcw.test2pay.com/fcw/zand/notify ；FCW Webhook Receiver 校验 HMAC，更新 CMF。
   - 域内：INST_STATUS=S，MEMO=Credited To Beneficiary，Type=OUTGOING_DOMESTIC_TRANSACTION_STATUS。
   - 国际：INST_STATUS=S，MEMO=PROCESSED，Type=OUTGOING_INTERNATIONAL_TRANSACTION_STATUS。
9. CMF 通过 router.t_channel_result_code 将银行结果码映射为 CMF 状态（result_status=S 等），将 tt_inst_order.STATUS 由 I 更新为 S/F。
10. DPM Accounting：扣减余额、登记手续费与账本（如国际 SWIFT 手续费 157.50 AED）。
11. Fundout Service：根据 CMF 最终结果，将 t_fundout_order.status 置为 SUCCESS 或 FAILURE。

## 涉及服务/表
服务/组件：
- SGS API Gateway
- Fundout Service
- Kafka MQ（topic: fundout.created / processing / status.update）
- CMF Router
- ZAND Bank APIs（SP / SQ / VS）
- FCW Webhook Receiver
- DPM Accounting
- BMOC Counter（结算审批）

数据表：
- mhtfundout.t_fundout_order（[[tbl_mhtfundout_t_fundout_order]]）：global_id, partner_id, status(CREATED/PLACED/SUCCESS/FAILURE), product_code, unity_result_code
- mhtfundout.t_fundout_bankcard_order（[[tbl_mhtfundout_t_fundout_bankcard_order]]）：fundout_crcy_code, fundout_amount, network_code, rate
- cmf.tt_inst_order（[[tbl_cmf_tt_inst_order]]）：INST_ORDER_NO, FUND_CHANNEL_CODE, STATUS(I/S/F/U), AMOUNT, RETRY_TIMES
- cmf.tt_inst_order_result（[[tbl_cmf_tt_inst_order_result]]）：API_TYPE(SP/SQ/VS), INST_STATUS, INST_SEQ_NO, EXTENSION, MEMO
- router.t_channel_result_code：channel_code, api_type, result_code, result_sub_code, result_status
- dpm.t_dpm_outer_account_subset：BALANCE, CURRENCY
- reconciliation.t_settlement_detail：settlement_status, settlement_amount, settlement_currency

产品码与渠道：220401->ZAND201；220402->ZAND203；230602->ZAND204/ZAND207/ZAND210。

## 校验点
- 下单：t_fundout_order 出现新行，product_code 与场景一致，unity_result_code 不为 cmf.route.fail。
- 路由：tt_inst_order.FUND_CHANNEL_CODE 为预期 ZAND 子渠道（避免误路由到 TEST201）。
- SP：tt_inst_order_result 存在 API_TYPE=SP 行，INST_STATUS=I，INST_SEQ_NO 为 D...（域内）或 ZIT...（国际），EXTENSION 含 CreationDateTime+ChannelRefId+channelTransTime。
- SQ（仅国际）：API_TYPE=SQ 行存在，ChannelRefId 与 SP 一致；轮询间隔随 RETRY_TIMES 增加，RETRY_TIMES=54 停止。
- VS：
  - 域内：API_TYPE=VS, INST_STATUS=S, ME
