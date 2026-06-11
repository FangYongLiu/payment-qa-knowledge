---
id: api_acquire2_dcc_quotation
object_type: API
name: "DCC 报价查询接口 (DirectPay Quotation Query)"
aliases: ["DCC Quotation", "DCC 报价", "Quotation Query API", "DCC资质", "dccQuoteId", "dccAvailable"]
domain: online-business
subdomain: acquire
module: DCC
status: active
owner: QA-Team
reviewer: Sijia.Zhang
last_reviewed_at: 2026-05-20
source_type: testcase
source_ref: "DCC_Via_CKO 01_E2E TC05/TC06/TC08; 03_Availability_Quotation TC12-TC19"
tags: ["DirectPay", "DCC", "quotation", "CKO", "FX"]
related_services: ["svc_acquireii", "svc_router"]
related_tables: ["tbl_merchant_dcc_config"]
related_scenarios: ["scn_dcc_accepted", "scn_dcc_not_eligible"]
related_logs: ["service:acquireii", "channel:CKO123"]
related_failures: ["ts_dcc_create_order_rejected"]
---

## 业务目的
DirectPay 模式下查询 DCC 报价。在报价处理中完成 DCC 资格判定(商户已开通 DirectPay DCC、provider=CKO_DCC_PFAC_01、卡币种≠AED 且不在黑名单、Metadata+FX 成功),并生成报价。

## 关键请求 / 响应字段
- 请求:订单金额、订单币种、reference、卡信息或 `cardToken`。
- 响应(资格满足):`dccAvailable=true`、`dccQuoteId`、`dccCurrency`、`dccAmount`、`exchangeRate`、`markUpRate`、`quoteExpiry`。

## 计算与精度
- `dccAmount = 订单金额 × exchangeRate × (1 + markUpRate)`。
- 精度按币种:USD 2 位、JPY 0 位、KWD/BHD 3 位。

## 测试步骤
1. 已开通商户 + 非 AED 合规卡 → 校验返回上述报价字段齐全且计算/精度正确。
2. `cardToken` 入参:系统解析回原卡再判定(TC06)。
3. 未开通商户 → 返回 `UNAUTHORIZED`/"api not authorized",且**不调** Metadata/FX(TC08/TC13)。
4. 入参校验错误码:`INVALID_ORDER_AMOUNT`/`INVALID_ORDER_CURRENCY`/`INVALID_REFERENCE`/`INVALID_CARD_NUMBER`/`INVALID_EXPIRY_MONTH`/`INVALID_EXPIRY_YEAR`。

## 预期结果
- 资格满足生成报价;`dccQuoteId` 有效期 **15 分钟**。
- 不满足任一资格条件 → 不出报价(详见 `scn_dcc_not_eligible`)。

## Kibana 校验
- `service:acquireii` 看资格判定;Router Channel Code=`CKO123`(Metadata/FX)。

## 常见风险 / 失败模式
- markup 超范围、币种精度错;FX 失败应导致不展示 DCC。
