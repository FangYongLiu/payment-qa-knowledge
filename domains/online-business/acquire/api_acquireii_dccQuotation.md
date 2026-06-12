---
id: api_acquireii_dccQuotation
object_type: API
domain: online-business
subdomain: acquire
module: DCC
status: draft
owner: e2e-demo@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-12'
source_type: wiki
source_ref: demo:e2e-real-pr-check
tags:
- DCC
- acquire
- quotation
- FX
sensitivity: normal
name: DCC 报价接口 dccQuotation
aliases:
- dccQuotation
- DCC 报价
- /sgs/api/acquire2/dccQuotation
related_services:
- svc_acquireii
- svc_router
related_tables:
- tbl_pay_order
- tbl_merchant_dcc_config
related_scenarios:
- scn_dcc_accepted
- scn_dcc_not_eligible
related_logs:
- service:acquireii
related_requirements: []
related_failures:
- ts_createOrder_quoteId_invalid
---

## 用途
持卡人在 PayPage 输入卡号后，runtime 触发 DCC（动态货币转换）资格判定。当卡 BIN 支持 DCC 且商户开通 DCC 时，调用本接口获取外币报价并展示给持卡人选择。

## 接口
- 方法/路径：`POST /sgs/api/acquire2/dccQuotation`
- 维护团队：acquire 收单团队

## 请求参数
- orderId
- 卡 BIN（前 8 位）
- 交易金额（AED）
- 币种

## 响应字段
- quoteId
- dccAmount（外币金额）
- exchangeRate（汇率，含 markup）
- markupRate（加价率）
- expireTime（有效期 15 分钟）

## 关键校验点（QA 要点）
1. 卡 BIN 不在 DCC 支持列表 → 返回 not eligible，不出报价。
2. markupRate 必须落在商户配置 `t_merchant_dcc_config` 的费率范围内（0 < rate < 1，最多 4 位小数）。
3. dccAmount = 交易金额(AED) × exchangeRate，且 exchangeRate 含 markup。
4. quoteId 必须能被 createOrder 正确引用；过期/篡改/不归属本单都要拒。

## 上下游
- 上游服务：acquireii（资格判定 + Metadata/FX）、router
- 落库：t_pay_order（markup、dccCurrency）、t_merchant_dcc_config（费率配置）

## 排障线索
- createOrder 因 quoteId 过期/不匹配被拒时，查看 `service:acquireii` 日志。
