---
id: flow_zand_fundout
object_type: Flow
name: ZAND渠道出款端到端流程(SP/SQ/VS)
aliases: [ZAND Fundout, zand-fundout-flow]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:AQ/2049867832
tags: [online-business, fundout, zand, SP, SQ, VS]
related_services: [svc_sgs, svc_fundout, svc_cmf, svc_fcw, svc_dpm_accounting, svc_merchant_fundout]
related_tables: [tbl_mhtfundout_t_fundout_order, tbl_mhtfundout_t_fundout_bankcard_order, tbl_cmf_tt_inst_order, tbl_cmf_tt_inst_order_result, tbl_router_t_channel_result_code]
related_scenarios: [scn_online_business_zand_fundout]
---

# ZAND渠道出款端到端流程(SP/SQ/VS)

## 概述
ZAND Fundout 指通过 ZAND 银行渠道将资金从 PayBy 账户转出至外部银行账户,覆盖境内(AED)、跨境(USD/SWIFT)、清结算与商户/个人提现。端到端链路:用户/商户发起出款 → Fundout Service 创建订单 → Kafka 异步 → CMF Router 路由到具体 ZAND 子渠道 → 调 ZAND Bank SP 提交支付 →(国际单)SQ 轮询 → VS Webhook 回调最终状态 → DPM 入账 → 订单置 SUCCESS/FAILURE。

入口包括:API 直连(合作商户)、Merchant Portal(转账/提现)、BMOC 清结算、Botim App 个人提现。

**渠道与产品码映射:**

| 场景 | 渠道 | 产品码 | 币种 | 时序模式 | 速度 |
|---|---|---|---|---|---|
| 境内 UAE 银行转账(IBAN AE 开头) via API | ZAND201 | 220401 | AED | SP→VS | ~12s |
| 跨境 SWIFT 转账 via API | ZAND203 | 220402 | USD | SP→SQ→VS | 小时级(异步) |
| 清结算境内转账 | ZAND204 | 230602 | AED | SP→VS | ~15s |
| 清结算跨境转账 | ZAND207 | 230602 | USD | SP→SQ→VS | 小时级(异步) |
| 商户后台提现(境内) | ZAND210 | 230602 | AED | SP→VS | ~12s |

**SP/SQ/VS 三阶段含义:** SP=Submit Payment(向 ZAND 提交,银行返回 ChannelRefId);SQ=Status Query(周期轮询查状态,仅国际);VS=Vendor Status Webhook(银行回调最终状态)。

## 步骤(跨系统)
1. **下单入口**:Client(Merchant Portal / Botim App / Partner API)发起转账或提现,经 [[svc_sgs]] 完成 Auth / Validation / Rate Limiting。
2. **订单创建**:[[svc_fundout]] 创建出款订单,执行 beneficiary 校验与 FX,写入 [[tbl_mhtfundout_t_fundout_order]](status=CREATED/PLACED)及 [[tbl_mhtfundout_t_fundout_bankcard_order]]、`t_fundout_beneficiary`(待补:beneficiary 表未单独建对象)。
3. **审批环节(条件)**:Merchant Portal 转账需在「My Authorization」授权后才处理;Settlement 流程需 BMOC 审计(Audit)通过后执行。
4. **异步路由**:Fundout Service 经 Kafka MQ(topic:`fundout.created` / `processing` / `status.update`)通知 CMF Router。
5. **CMF 路由**:[[svc_cmf]] 按 partner 配置与产品码路由到具体渠道,写入 [[tbl_cmf_tt_inst_order]](INST_ORDER_NO 如 `ZAND20326031611337631`,STATUS=I)。
6. **SP 提交支付**:CMF 调 ZAND Bank SP API,银行返回 ChannelRefId(境内 `D...` / 国际 `ZIT...`);在 [[tbl_cmf_tt_inst_order_result]] 写一行 `API_TYPE=SP`、`INST_STATUS=I`、`INST_SEQ_NO=ChannelRefId`、`EXTENSION` 含 CreationDateTime + ChannelRefId + channelTransTime。SP 失败/超时 → retry handler(指数退避)→ retry queue → worker 重提;永久失败则冲销手续费。
7. **SQ 轮询(仅国际)**:CMF 周期调 ZAND Bank SQ API。前 ~2 分钟密集,间隔逐步增大;`RETRY_TIMES > 35` 后达小时级;`RETRY_TIMES = 54` 停止。每次写 `API_TYPE=SQ` 行,`INST_STATUS=I` 或 `S`,ChannelRefId 与 SP 一致。
8. **VS 回调**:ZAND Bank 调 [[svc_fcw]] Webhook(`https://uat-fcw.test2pay.com/fcw/zand/notify`),FCW 校验 HMAC 后写 `API_TYPE=VS` 行:
   - 境内:`INST_STATUS=S`,`MEMO=Credited To Beneficiary`,Type=`OUTGOING_DOMESTIC_TRANSACTION_STATUS`
   - 国际:`INST_STATUS=S`,`MEMO=PROCESSED`,Type=`OUTGOING_INTERNATIONAL_TRANSACTION_STATUS`
9. **状态映射**:CMF 通过 [[tbl_router_t_channel_result_code]](channel_code + api_type + result_code/sub_code → result_status)把银行结果码映射为 CMF `STATUS=S/F`。
10. **入账**:CMF 置 `STATUS=S` 后,[[svc_dpm_accounting]] 扣减余额并登记手续费/台账(国际 SWIFT 例如手续费 157.50 AED);结算记录落 `reconciliation.t_settlement_detail`(待补:该表未单独建对象)。
11. **终态**:`t_fundout_order.status` 置为 SUCCESS 或 FAILURE。

## 关联关系
- **经过的服务(有序)**:[[svc_sgs]] → [[svc_fundout]] → [[svc_cmf]] → ZAND Bank → [[svc_fcw]] → [[svc_dpm_accounting]](= `related_services`);商户出款入口另经 [[svc_merchant_fundout]]。
- **关键表**:[[tbl_mhtfundout_t_fundout_order]]、[[tbl_mhtfundout_t_fundout_bankcard_order]]、[[tbl_cmf_tt_inst_order]]、[[tbl_cmf_tt_inst_order_result]]、[[tbl_router_t_channel_result_code]](= `related_tables`)
- **关键场景**:[[scn_online_business_zand_fundout]](= `related_scenarios`);排障见 [[ts_zand_fundout]];Mock VS 工具 [[auto_online_business_zand_mock_vs]]

## 单据号与引用号格式
| 类型 | 格式 | 示例 |
|---|---|---|
| 境内 ZAND reference | 以 `D` 开头 | `D773644227520987` |
| 跨境 ZAND reference | 以 `ZIT` 开头 | `ZIT3657863264122` |
| CMF 订单号 | `ZAND` + 渠道号开头 | `ZAND20326031611337631` |
| Fundout 订单 ID | 18 位数字 | `131773657853407506` |

## 校验点
- **路由**:`t_fundout_order.unity_result_code` 非 `cmf.route.fail`;CMF `FUND_CHANNEL_CODE` 命中预期渠道(ZAND201/203/204/207/210),未误路由到 `TEST201`。
- **SP 行**:`INST_STATUS=I`;`INST_SEQ_NO` 为 ChannelRefId(境内 `D...` / 国际 `ZIT...`);`EXTENSION` 含 CreationDateTime + ChannelRefId + channelTransTime。
- **SQ 行(仅国际)**:ChannelRefId 与 SP 一致;EXTENSION 与 SP 一致;`INST_STATUS=I` 或 `S`;轮询间隔随次数增加,`RETRY_TIMES=54` 停止。
- **VS 行**:境内 `MEMO=Credited To Beneficiary`、国际 `MEMO=PROCESSED`,均 `INST_STATUS=S`。
- **入账**:`dpm.t_dpm_outer_account_subset.BALANCE` 正确扣减(含手续费)。
- **EXTENSION 一致性**:SP/SQ/VS 三阶段以 `INST_SEQ_NO`(`D.../ZIT...`) 为关键字横向比对 CreationDateTime / ChannelRefId / channelTransTime,不一致通常意味着串单或回调错配。
