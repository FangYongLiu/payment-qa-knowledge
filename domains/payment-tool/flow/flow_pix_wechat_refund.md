---
id: flow_pix_wechat_refund
object_type: Flow
name: PIX 微信渠道退款流程(含退款推定)
aliases: [微信退款, pix-wechat refund]
domain: payment-tool
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:PMDPayment/433881954
tags: [pix, wechat, refund, 退款, mpc, 退款推定]
related_services: []
related_tables: []
related_scenarios: [scn_pix_wechat_vendor_api]
---

# PIX 微信渠道退款流程(含退款推定)

## 概述
微信 MPC 渠道退款:由 pix 实现 vendor api,对退款做必要校验后**异步**发起退款请求并向 vendor 返回成功。微信侧对退款结果**不提供异步通知**,需通过 `QUERY_REFUND_ORDER_INFO` 在 10 分钟内主动查询;超过该窗口仍无结果时调 `NOTIFY_PRESUPPTIVE_REFUND_SUCCESS` 进行**退款推定**(默认仅推定通知 1 次,一旦推定即按退款成功处理)。钱包侧可通过次日账单获取推定的交易记录。退款资金流通过 reconciliation 配置对账。
服务对象 svc_pix 待补。

## 步骤(跨系统)
1. **refund**(Vendor Responder `REFUND`):外商 → Tenpay apply refund → Tenpay → pix refund;pix → tradeii 执行退款处理;做必要校验,异步请求退款,向 vendor 返回成功;通知退款账单(notify refund bill,pix → query)。
   - 退款金额:`Refund pay amount = Refund transaction amount / Original transaction amount × Original pay amount`(按原单成交比例折算,避免重新走汇率)。
   - 允许退款失败(refund fail allowed = Yes)。
2. **query refund**(Vendor `QUERY_REFUND_ORDER_INFO`):pix 查本地退款状态;微信在 10 分钟内通过该 API 查询退款结果。
3. **notify final refund / 推定**(Vendor `NOTIFY_PRESUPPTIVE_REFUND_SUCCESS`):多次查询且约 10 分钟仍无结果时执行推定;默认只推定通知 1 次,一旦推定按退款成功处理。
4. **bill / reconciliation**:退款账单同步(pix);bill 配置(bill 服务);退款对账配置(reconciliation 服务)。

## 关联关系
- **经过的服务(有序)**:Tenpay → pix → tradeii / query / bill / reconciliation(服务对象待补)
- **关键场景 / 参考**:[[scn_pix_wechat_vendor_api]]
- **主流程**:[[flow_pix_wechat_mpc_payment]];对账 [[flow_pix_wechat_reconciliation]]

## 校验点
- 退款发起前需做必要校验(Do necessary check of refund)。
- 退款金额换算公式正确性。
- 退款结果获取方式:无异步通知,依赖 QUERY_REFUND_ORDER_INFO 在 10 分钟窗口内查询。
- 推定触发:多次查询且约 10 分钟无结果;推定通知默认仅 1 次;一旦推定按退款成功处理。
- 钱包通过次日账单获得推定交易记录。
