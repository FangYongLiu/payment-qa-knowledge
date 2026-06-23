---
id: flow_zand_fundout
object_type: Flow
domain: fund-out-transfer
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: wiki:7f334321-3b49-4c87-b6d9-8949925a962a
tags:
- zand
- fundout
- SP
- SQ
- VS
subdomain: zand-channel
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
- tbl_router_t_channel_result_code
related_scenarios:
- scn_zand_fundout_test_cases
related_logs: []
related_requirements: []
related_failures: []
---

## 概述
ZAND渠道Fundout端到端流程：从用户/商户发起出款，到 Fundout Service 创建订单，CMF Router 路由到对应银行渠道，调用 ZAND Bank SP 提交支付，国际单据由 SQ 轮询，最终由 VS Webhook 回调驱动 DPM 入账，订单标记 SUCCESS/FAILED。

适用渠道：ZAND201（域内 AED ~12s）、ZAND203（SWIFT USD 异步）、ZAND204（结算域内）、ZAND207（结算国际）、ZAND210（商户门户域内提现）。

时序模式：
- Domestic：SP -> VS（无需 SQ）
- International：SP -> SQ（轮询）-> VS（最终）

## 步骤(跨系统)
1. **下单入口**：Client（Merchant Portal / Botim App / Partner API）发起转账，经 SGS API Gateway 完成 Auth、Validation、Rate Limiting。
2. **订单创建**：Fundout Service 创建出款订单，写入 `mhtfundout.t_fundout_order`（status=CREATED）及 `t_fundout_bankcard_order`、`t_fundout_beneficiary`；执行 beneficiary checks、FX。
3. **审批环节（条件）**：
   - Merchant portal 转账：需 My Authorization 授权后方可处理
   - Settlement 流程：需 BMOC 审计通过后执行
4. **异步路由**：Fundout Service 通过 Kafka MQ（topic：fundout.created / processing / status.update）通知 CMF Router。
5. **CMF 路由**：CMF Router 根据 partner 配置与产品码（220401 / 220402 / 230602）路由到具体渠道（ZAND201/203/204/207/210），写入 `cmf.tt_inst_order`（STATUS=I）。
6. **SP 提交支付**：CMF 调用 ZAND Bank SP API，银行返回 ChannelRefId（域内 D... / 国际 ZIT...）。在 `tt_inst_order_result` 写入一行 API_TYPE=SP，INST_STATUS=I，INST_SEQ_NO=ChannelRefId，EXTENSION 包含 CreationDateTime + ChannelRefId + channelTransTime。
   - SP 失败/超时 -> retry handler（指数退避）-> retry queue -> worker 重提交；永久失败回滚手续费。
7. **SQ 轮询（仅国际）**：CMF 周期调用 ZAND Bank SQ API。
   - 前 ~2 分钟密集轮询，随后间隔逐步增大
   - RETRY_TIMES > 35：间隔达到小时级
   - RETRY_TIMES = 54：停止轮询
   - 每次写入 API_TYPE=SQ 行，INST_STATUS=I 或 S，ChannelRefId 与 EXTENSION 同 SP 一致。
8. **VS 回调**：ZAND Bank 调用 FCW Webhook（uat-fcw.test2pay.com/fcw/zand/notify）。
   - FCW 校验 HMAC 签名
   - 写入 API_TYPE=VS 行：
     - 域内：INST_STATUS=S，MEMO=Credited To Beneficiary，Type=OUTGOING_DOMESTIC_TRANSACTION_STATUS
     - 国际：INST_STATUS=S，MEMO=PROCESSED，Type=OUTGOING_INTERNATIONAL_TRANSACTION_STATUS
9. **状态映射**：通过 `router.t_channel_result_code`（channel_code + api_type + result_code/sub_code -> result_status）映射为 CMF STATUS=S。
10. **入账**：FCW 通知 CMF 更新 STATUS=S 后，DPM Accounting 执行余额扣减并入账（国际单还涉及手续费，例如 SWIFT 157.50 AED）。
11. **终态**：`t_fundout_order.status` 更新为 SUCCESS 或 FAILURE。

## 涉及服务/表
**服务/组件**
- SGS API Gateway：鉴权、校验、限流
- Fundout Service：订单创建、受益人校验、FX
- Kafka MQ：fundout.created / processing / status.update
- CMF Router：渠道路由与指令订单管理
- ZAND Bank APIs：SP / SQ / VS
- FCW Webhook Receiver：HMAC 校验、回写 CMF
- DPM Accounting：余额、手续费、账务

**数据库表**
- [[tbl_mhtfundout_t_fundout_order]] 出款主单（global_id, partner_id, status, product_code, unity_result_code）
- [[tbl_mhtfundout_t_fundout_bankcard_order]] 银行卡明细（fundout_crcy_code, fundout_amount, network_code, rate）
- [[tbl_cmf_tt_inst_order]] CMF 渠道指令（INST_ORDER_NO, FUND_CHANNEL_CODE, STATUS, AMOUNT, RETRY_TIMES）
- [[tbl_cmf_tt_inst_order_result]] SP/SQ/VS 结果（API_TYPE, INST_STATUS, INST_SEQ_NO, EXTENSION, MEMO）
- [[tbl_router_t_channel_result_code]] 银行返回码 -> CMF 状态映射
- dpm.t_dpm_outer_account_subset：账户余额
- reconciliation.t_settlement_detail：结算记录

## 校验点
- **路由**：t_fundout_order.unity_result_code 非 cmf.route.fail；CMF 中 FUND_CHANNEL_CODE 命中预期渠道（ZAND201/203/204/207/210），未误路由到 TEST201。
- **SP 行**：INST_STATUS=I；INST_SEQ_NO 为 ChannelRefId（域内 D... / 国际 ZIT...）；EXTENSION 含 CreationDateTime + ChannelRefId + channelTransTime。
- **SQ 行（国际）**：ChannelRefId 与 SP 一致；EXTENSION 与 SP 一致；INST_STATUS=I 或 S；轮询间隔随次数增加，RETRY_TIMES=54 停止。
- **VS 行**：
  - 域内：INST_STATUS=S，MEMO=Credited To Beneficiary，Type=OUTGOING_DOMESTIC_TRANSACTION_STATUS
  - 国际：IN
