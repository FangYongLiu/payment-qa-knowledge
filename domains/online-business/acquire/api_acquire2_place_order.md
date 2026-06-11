---
id: api_acquire2_place_order
object_type: API
name: "PayPage 下单接口 (placeOrder)"
aliases: ["placeOrder", "/sgs/api/acquire2/placeOrder", "PayPage 下单", "HPP 下单", "paySceneCode PAYPAGE"]
domain: online-business
subdomain: acquire
module: DCC
status: active
owner: QA-Team
reviewer: Sijia.Zhang
last_reviewed_at: 2026-05-20
source_type: testcase
source_ref: "DCC_Via_CKO_Integration_Test_Case 01_E2E_DCC_MainFlow TC01/TC03/TC04"
tags: ["DirectPay", "DCC", "PayPage", "CKO", "placeOrder"]
related_services: ["svc_acquireii", "svc_tradeii"]
related_tables: ["tbl_acquireii_t_acquire_order", "tbl_tradeii_t_trade_order", "tbl_tradeii_t_pay_order"]
related_scenarios: ["scn_dcc_accepted", "scn_dcc_declined", "scn_dcc_not_eligible"]
related_logs: ["service:acquireii", "service:tradeii", "channel:CKO123", "channel:CKO302"]
---

## 业务目的
PayPage(HPP)收银台的下单入口。`POST /sgs/api/acquire2/placeOrder`,`paySceneCode=PAYPAGE`,返回 `tokenUrl`(PayPage 地址)。持卡人在 PayPage 输卡后点 Pay,runtime 触发 DCC 资格判定。

## 关键请求 / 响应字段
- 请求:`paySceneCode=PAYPAGE`、订单金额/币种、商户信息。
- 响应:`tokenUrl`(有效 PayPage URL)。

## 测试步骤
1. 调 placeOrder(PAYPAGE)→ 校验返回 success + 合法 tokenUrl。
2. 打开 PayPage 输入卡号(如 4273149019799094 / 12/31 / CVV 123)→ 点 Pay。
3. runtime 触发 DCC 资格判定(见 `api_acquire2_dcc_quotation` 与 `scn_dcc_not_eligible` 的判定条件)。
4. 资格满足展示 DCC 选择页;Accept 走外币、Decline 走商户币;3DS 密码 `Checkout1!`。

## 预期结果
- 返回 tokenUrl;DCC 满足时展示选择页(订单金额 AED、DCC 外币金额、汇率、markup),无默认选项。
- 提交后 `dccUptake=ACCEPTED|DECLINED`,支付成功展示结果页。

## DB 校验
- `tbl_acquireii_t_acquire_order`、`tbl_tradeii_t_trade_order`、`tbl_tradeii_t_pay_order`(dcc 字段)。

## Kibana 校验
- `service:acquireii` 看资格判定;Router Channel Code:Metadata/FX=`CKO123`,支付=`CKO302`。

## 常见风险 / 失败模式
- Metadata/FX API 失败 → 应跳过 DCC 走正常流程,不应展示选择页。
