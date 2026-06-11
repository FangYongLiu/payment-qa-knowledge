---
id: flow_dcc_checkout
object_type: Flow
name: "DCC 收银端到端流程 (E2E)"
aliases: ["DCC流程", "DCC收银", "DCC E2E", "dcc checkout flow", "DCC 端到端"]
domain: online-business
subdomain: acquire
module: DCC
status: active
owner: QA-Team
reviewer: Sijia.Zhang
last_reviewed_at: 2026-05-20
source_type: testcase
source_ref: "DCC_Via_CKO 01_E2E_DCC_MainFlow (PayPage/DirectPay end-to-end)"
tags: ["DCC", "flow", "E2E", "checkout"]
related_services: ["svc_acquireii", "svc_tradeii", "svc_router"]
related_tables: ["tbl_acquireii_t_acquire_order", "tbl_tradeii_t_trade_order", "tbl_tradeii_t_pay_order"]
related_scenarios: ["scn_dcc_accepted", "scn_dcc_declined", "scn_dcc_not_eligible"]
related_logs: ["service:acquireii", "service:tradeii", "channel:CKO123", "channel:CKO302"]
---

## 流程概述
DCC via CKO 的完整收单链路,覆盖 PayPage 与 DirectPay。

## 主要步骤
1. **下单/报价**:PayPage 走 `api_acquire2_place_order`;DirectPay 走 `api_acquire2_dcc_quotation`。
2. **资格判定**(acquireii):开通+provider CKO+卡币种≠AED+非黑名单+Metadata/FX 可用。
3. **Metadata + FX**(Router `CKO123`):取卡币种与汇率,算 `dccAmount = 金额 × rate × (1+markup)`。
4. **展示选择页 / 用户选择**:ACCEPTED(外币)或 DECLINED(商户币)。
5. **创建订单**:`api_acquire2_create_order` 带 currencyConversion;出账走 Router `CKO302`。
6. **落库**:acquireii.t_acquire_order → tradeii.t_trade_order / t_pay_order(DCC 字段)。
7. **后续**:Get Order / 异步通知 / Portal / 结算 / 对账(对账结算见模块 5)。
8. **退款/取消**:`api_acquire2_refund`(按原汇率/末笔差额、含取消全额冲正)。

## 涉及服务
- `svc_acquireii`(资格/报价/下单/退款入口)、`svc_tradeii`(落单)、`svc_router`(CKO 路由)。

## 涉及表
- `tbl_acquireii_t_acquire_order`、`tbl_tradeii_t_trade_order`、`tbl_tradeii_t_pay_order`。

## 常见风险 / 失败模式
- 报价过期/汇率漂移;acquireii→tradeii 异步消息丢失致订单卡处理中;出账金额/币种与用户所选不一致。
