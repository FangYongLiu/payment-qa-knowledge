---
id: scn_online_business_auto_debit
object_type: Scenario
name: 自动代扣 / 签约 (Auto Debit)
aliases: []
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-03'
source_type: repo
source_ref: cgs-apitest/testcases/payment/toB/test_auto_debit_fangyong.py (UAT 实跑 2026-07-03)
tags: [online-business, 支付, cgs-apitest, 实测]
related_services: [svc_authpay, svc_deduct, svc_tradeii, svc_payment, svc_member, svc_cards]
related_tables: [tbl_deduct_t_deduct_protocol_config, tbl_deduct_t_deduct_protocol_apply, tbl_deduct_t_deduct_protocol, tbl_protocol_t_contract_sign_info]
related_logs: []
---

# 自动代扣 / 签约 (Auto Debit)

> 业务测试场景。来源 cgs-apitest 回归。穿过 payment-core 交易/支付核心。

## 场景描述
toB 自动代扣:基于签约(sign_contract_no)+ 代扣渠道(deductChannelId)用余额/银行卡/余额+卡组合扣款,含扣款失败与退款。经 authpay 授权 + deduct 执行 → tradeii/payment。

## 关联关系
- **涉及服务**:[[svc_authpay]]、[[svc_deduct]]、[[svc_tradeii]]、[[svc_payment]]、[[svc_member]]、[[svc_cards]](= `related_services`,穿过的服务链)
- **覆盖的自动化**:由覆盖本场景的 AutomationAsset 在其 `related_scenarios` 中声明。
- **读写的表**:[[tbl_deduct_t_deduct_protocol_config]](扣款服务配置)、[[tbl_deduct_t_deduct_protocol_apply]](签约记录)、[[tbl_deduct_t_deduct_protocol]](已签约代扣协议号)、[[tbl_protocol_t_contract_sign_info]](签订信息)。
- **收单入口**:PAYANDSIGN(支付并签约)/ AUTODEBIT 下单参数样例见 [[reference_acquire_payscene_request_examples]]。

## 签约 → 代扣 数据链路(PAYANDSIGN / AUTODEBIT)
1. **配置扣款服务**:`protocolSceneCode`(PAYANDSIGN 参数)= 自动扣款服务 ID;配置表 [[tbl_deduct_t_deduct_protocol_config]] 的 `protocol_scene_code`(常量 `120`,SIM 测试 `111`)。商户须先在 Basis 配置内部代扣才可下单:`Basis → DataConfig → MerchantConfig → Merchant Setting`。
2. **申请并签约**:先申请签约协议,用户登录 App 确认签约 → 成功后:
   - [[tbl_deduct_t_deduct_protocol_apply]] 商户签约记录(`status=S` 成功)`deduct_protocol_no`。
   - [[tbl_deduct_t_deduct_protocol]] 已签约可用代扣协议号(`status=A` 可用)`deduct_protocol_no`。
   - [[tbl_protocol_t_contract_sign_info]] 签订信息(`status=EFFECTIVE` 有效)`sign_contract_no`(如 `2520250424112248107256`)。
3. **代扣下单**:AUTODEBIT 的 `authProtocolNo` = `deduct.t_deduct_protocol.deduct_protocol_no`。

## 实测(UAT 2026-07-03,test_auto_debit,商户 200000080798)
- **AUTODEBIT product = "Auto Debit"**;`test_autodebit_balance` / `_bankcard` / `_balance_refund` 均 SETTLED,余额扣款 `payChannel=BALANCE`、`payerMid=100000081325`、payee_fee 0.01/0.11。
- **签约申请**:`cashdesk/protocol/querySimpleApply` 返回签约模板 `templateNo=02001`、`applyVoucherNo`、`signerId`(付款人)、`merchantId`、`partnerId=200000000042`(PayBy 平台)——即 PAYANDSIGN → AUTODEBIT 前的用户签约确认。
- 下单参数 `authProtocolNo` = 签约成功后的 `deduct.t_deduct_protocol.deduct_protocol_no`(见上「签约链路」)。

## 校验点(QA)
- 余额/银行卡/组合扣款成功与失败(N104/105)分支。
- 签约 contract_no 有效性;deductChannelId 路由。
- 扣款后退款;落库扣款单状态。

## 来源与置信
- cgs-apitest payment 套件整理;服务链由调用线索+callgraph 推断,部分标待补。
