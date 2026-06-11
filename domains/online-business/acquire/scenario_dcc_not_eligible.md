---
id: scn_dcc_not_eligible
object_type: Scenario
name: "DCC 不可用 (Not Eligible) 走正常流程"
aliases: ["DCC Not Eligible", "DCC不可用", "不展示DCC", "AED卡", "黑名单", "Metadata失败", "FX失败"]
domain: online-business
subdomain: acquire
module: DCC
status: active
owner: QA-Team
reviewer: kai.wang
last_reviewed_at: 2026-05-20
source_type: testcase
source_ref: "DCC_Via_CKO 01_E2E TC04; 03_Availability_Quotation TC01-TC07"
tags: ["DCC", "not-eligible", "boundary"]
related_services: ["svc_acquireii", "svc_router"]
related_tables: ["tbl_merchant_dcc_config", "tbl_tradeii_t_trade_order"]
related_logs: ["service:acquireii", "channel:CKO123"]
---

## 前置条件(任一即不可用)
- 商户未开通 DCC 产品;或 provider≠CKO;
- 卡币种=AED;或卡币种在 DCC 黑名单;
- Get Card Metadata API 失败;或 FX Rate API 失败。

## 步骤
1. 发起支付/报价。
2. 系统执行 DCC 资格判定。

## 预期结果
- **不展示** DCC 选择页,不提示选币种;支付按正常流程,交易币种=AED/原始币种。
- 卡币种=AED 时**不调** FX;Metadata/FX 失败时跳过 DCC 继续正常流程。
- 无 DCC 字段作为交易金额。

## DB 校验
- `tbl_tradeii_t_trade_order`:`dccUptake=NULL/NOT_APPLICABLE`,无 DCC 金额/markup 落库为交易金额。

## Kibana 校验
- `service:acquireii` 看判定为不可用;`channel:CKO123` 失败时的降级日志。

## 关联配置
- `tbl_merchant_dcc_config`(provider、币种黑/白名单、是否开通)。
