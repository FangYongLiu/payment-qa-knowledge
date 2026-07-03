---
id: reference_fundout_channel_mock_rules
object_type: Reference
name: 出款/转账测试 —— 渠道 Mock 触发规则 + 请求样例
aliases: [funchannel-mock, fundout mock, 出款mock规则, transfer request examples, TransferToBank]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-03'
source_type: 有道云笔记(商户端2025) QA 实操整理
source_ref: 'PDF: 商户端系2025 (有道云笔记, QA 出款/转账实操, 2024-2025)'
tags: [online-business, fundout, transfer, mock, 测试数据, 出款]
related_services: [svc_cmf, svc_router]
related_scenarios: [scn_online_business_merchant_payout]
---

# 出款/转账测试 —— 渠道 Mock 触发规则 + 请求样例

测商户出款 / 转账(merchant payout / transfer)时,用**模拟资金渠道 `funchannel-mock`(`gp999_funchannel-mock`,测试渠道如 `TEST101` / `TEST201`)**按输入触发指定结果。经 [[svc_cmf]] → [[svc_router]] 路由到 mock 渠道。出款业务场景见 [[scn_online_business_merchant_payout]],端到端流程见 [[flow_merchant_fundout]]。

> 用途:构造出款/退款/转账的**成功、处理中、各类失败**分支,覆盖 [[svc_merchant_fundout]] 及渠道侧异常处理。仅测试环境。

## Mock 规则 A —— 由「卡有效期」触发(EXPIRED_DATE_MAP)
| expMonth / expYear | 触发结果 |
| --- | --- |
| `04`/`27`(或 `4`/`27`) | EXPIRED_CARD |
| `05`/`22`(或 `5`/`22`) | DECLINED |
| `02`/`37`(或 `2`/`37`) | UNSPECIFIED_FAILURE |

## Mock 规则 B —— 由「金额区间」触发(AMOUNT_RANGE_MAP)
| 金额区间(AED) | 触发结果 |
| --- | --- |
| 0 – 0.01 | AMOUNT_TOO_SMALL |
| 10000 – 15000 | IN_PROCESS(处理中) |
| 15000 – 20000 | CHANNEL_ERROR |
| 20000 – 25000 | INSUFFICIENT_FUNDS |
| 25000 – 30000 | AMOUNT_EXCEED |
| 30000 – 35000 | INFO_ERROR |
| 35000 – 40000 | CARD_NO_ERROR |
| 40000 – 45000 | NOT_TRANSACTION_TIME |
| 45000 – 50000 | TRANS_NUM_EXCEED |
| 50000 – 55000 | CHANNEL_REFUSED |
| 55000 – 60000 | TRANSACTION_FAILED |
| 60000 – 65000 | CARD_STATUS_ERROR |

> 写用例时:选目标结果对应的**金额或有效期**即可稳定复现该分支;`IN_PROCESS` 用于测「卡在处理中」的人工处理路径,见 [[ts_fundout_stuck_in_process]]。

## 转账 / 出款请求样例
接口前缀 `/sgs/api/transfer/...`。测试商户:SIM `200000429066`,UAT `200000079697`(转卡 UAT `200000082711`)。测试渠道 `TEST201`。

**转账到钱包 placeTransferOrder**:`amount` + `beneficiaryIdentity`(加密,`beneficiaryIdentityType=PHONE_NO`)+ `beneficiaryFullName`(加密)+ `merchantOrderNo` + `notifyUrl`。

**转账到 IBAN placeTransferToBankOrder**(本地 AED,产品码 `220401`):
```json
{ "merchantOrderNo": "M$random12", "swiftCode": "BBMEAEAD",
  "iban": "加密|AE470200000012213138001", "holderName": "加密|FANGYONG LIU",
  "networkCode": "LOCAL", "countryCode": "UAE", "fundoutCurrencyCode": "AED",
  "beneficiaryType": "IBAN", "beneficiaryAddress": "加密|Sky Tower 26 F",
  "amount": { "currency": "AED", "amount": 10.01 }, "memo": "company single pay" }
```
- SWIFT USD(产品码 `220402`):`networkCode=SWIFT`、`accountNo`(加密)、`beneficiaryType=BBAN`、`fundoutCurrencyCode=USD`。

**转账到卡 placeTransferToBankCard**:支持 `cardNumber`(加密)或 `cardToken`;含 `accountHolderType=INDIVIDUAL`、`senderType`、`senderInfoRequest`(sourceOfFunds/dateOfBirth 等)。注:sender 的 `CORPORATE` 上游 frontend 已支持、渠道侧未支持;payee 的 `CORPORATE` 完全不支持。

## QA 关注点
- **失败分支覆盖**:用金额区间 / 有效期 map 逐一造 CHANNEL_ERROR / INSUFFICIENT_FUNDS / CARD_STATUS_ERROR 等,验证 [[svc_merchant_fundout]] 与订单状态流转、账户资金回退。
- **处理中(IN_PROCESS)**:cmf 订单默认保持 process(避免资金亏损),需走人工处理 → [[ts_fundout_stuck_in_process]]。
- **转账类型矩阵**:IBAN(LOCAL AED)/ SWIFT(USD)/ 卡(卡号或 token);CORPORATE sender/payee 的支持度差异是重要边界。
- CKO 转卡回调(`TransferToCardNotification`)地址按环境配置(SIM/UAT `.../fcw/server/CKO201-VS/{data.reference}/notify.do`);结果异步,支付后需等回调更新。
