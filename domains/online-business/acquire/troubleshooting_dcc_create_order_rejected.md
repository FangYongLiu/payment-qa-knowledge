---
id: ts_dcc_create_order_rejected
object_type: Troubleshooting
name: "DCC 创建订单被拒 / 报价类报错排查"
aliases: ["创建订单被拒", "quote过期", "quoteId不匹配", "报价篡改", "UNAUTHORIZED", "DCC下单失败排查"]
domain: online-business
subdomain: acquire
module: DCC
status: active
owner: QA-Team
reviewer: Sijia.Zhang
last_reviewed_at: 2026-05-20
source_type: testcase
source_ref: "DCC_Via_CKO 01_E2E TC08-TC12 (create order rejections)"
tags: ["DCC", "troubleshooting", "reject"]
related_services: ["svc_acquireii"]
related_scenarios: ["scn_dcc_not_eligible"]
related_logs: ["service:acquireii"]
related_failures: []
---

## 症状
DirectPay Create Order 被拒,或报价/资格类报错。

## 可能根因与定位
- **UNAUTHORIZED / "api not authorized"**:商户未开通 DirectPay DCC(查 `tbl_merchant_dcc_config` / 产品开通状态)。
- **dccQuoteId 过期**:报价有效期 15 分钟,超时即拒(看下单与报价时间差)。
- **quoteId 不属于当前 partnerId**:用了别的商户的报价。
- **quoteId 与卡不匹配**:报价用卡 A、下单用卡 B。
- **报价数据篡改**:`dccCurrency/dccAmount/markUpRate/exchangeRate` 与 quoteId 绑定的报价不一致。
- 上述校验在 Create Order 校验阶段拦截,**不进入下游处理**,不创建订单。

## 排查步骤
1. 看 `service:acquireii` 校验日志定位拒因(归属/匹配/过期/篡改/未授权)。
2. 核对 `tbl_merchant_dcc_config` 开通与 provider。
3. 重新走报价拿新 `dccQuoteId`,确保卡与商户一致、字段原样回传。

## 相似历史
- 报价过期未刷新导致锁汇率失败;前端缓存旧报价。
