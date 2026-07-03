---
id: reference_acquire_payscene_request_examples
object_type: Reference
name: 收单下单各场景请求样例手册 (acquire2/placeOrder by paySceneCode)
aliases: [paySceneParams examples, 下单请求样例, placeOrder examples, 收单场景参数样例]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-03'
source_type: 有道云笔记(商户端2025) QA 实操整理
source_ref: 'PDF: 商户端系2025 (有道云笔记, QA 收单实操, 2024-2025)'
tags: [online-business, acquiring, SGS, paySceneCode, 测试用例, 请求样例]
related_services: [svc_sgs, svc_acquireii]
related_scenarios: [scn_online_business_direct_pay, scn_online_business_pre_auth, scn_online_business_auto_debit, scn_online_business_cashier_pay, scn_online_business_mpgs_channel]
---

# 收单下单各场景请求样例手册 (acquire2/placeOrder by paySceneCode)

QA 实操整理的 [[api_sgs_acquire_place_order]] 各 `paySceneCode` **真实请求体样例 + 测试商户/测试卡**,可直接改写成数据驱动用例 / 自动化。字段规则见 [[reference_acquire_protocol_and_codes]];测试卡见 [[reference_mpgs_test_cards]] / [[reference_cko_test_cards]]。

> 约定:敏感字段(cardNo/holderName/cvv/expYear 等)传 `加密|<明文>`(SDK 加密);金额 `Money={currency,amount}`;`merchantOrderNo` 唯一(示例用 `M$random12`)。以下为**测试环境(SIM/UAT)**样例,禁用于生产。

## PAYPAGE(支付网页 / 收银台)
```json
"paySceneCode": "PAYPAGE",
"paySceneParams": { "redirectUrl": "https://www.yoursite.com", "customerId": "",
  "changePayer": "True", "oneTimePayment": "False",
  "email": "test@example.com", "eid": "784199729481194" }
```
- 支持移动端 / PC 打开链接完成支付;返回 `tokenUrl`。
- **AFT 商户**(账户资金转账)示例:`200000429462`,请求体含 `accountFundingParameter`(purpose=`CRYPTOCURRENCY_PURCHASE`、recipient/sender 的 account/address/identification/nameDetails、senderType=`COMMERCIAL_ORGANIZATION`)。

## INAPP(商户 App 集成 SDK)
```json
"paySceneCode": "INAPP",
"paySceneParams": { "iapDeviceId": "deviceId123", "appId": "20241005000000411",
  "email": "test@example.com", "eid": "784199729481194" }
```
- `appId` 从 [Setting → Developers → My Apps] 取。SIM appId `20241005000000601` / UAT appId `20241005000000411`;`iapDeviceId`=付款人设备 ID。

## DYNQR(商家动态二维码,用户扫)
```json
"paySceneCode": "DYNQR",
"paySceneParams": { "changePayer": "true", "oneTimePayment": "",
  "email": "test@example.com", "eid": "<SHA256 或明文>" }
```

## EWALLET(Deeplink 拉起目标钱包)
```json
"paySceneCode": "EWALLET",
"paySceneParams": { "eWalletCode": "payby", "osType": "IOS", "terminalType": "APP",
  "redirectUrl": "http://www.example.com", "oneTimePayment": "", "eid": "784199729481194" }
```
- 返回 `deepLink`;`eWalletCode` 枚举见协议速查。

## QRPAY(用户出示付款码,商户扫)
```json
"paySceneCode": "QRPAY",
"paySceneParams": { "authCode": "<付款码数据>" }
```

## DIRECTPAY(直联 / 绑卡 / MOTO / ApplePay / DCC / PayFacs)
**首次卡支付**:
```json
"paySceneCode": "DIRECTPAY", "payeeMid": "200000429457",
"paySceneParams": { "cardNo": "加密|5123450000000008", "holderName": "加密|FANGYONG LIU",
  "expYear": "39", "expMonth": "01", "cvv": "加密|100", "platformType": "WEB",
  "threeDSecure": "false", "customerId": "987654321", "realIP": "222.64.177.132",
  "saveCard": "true", "redirectUrl": "https://www.example.com" }
```
- **MOTO**:走 DIRECTPAY,AFT 商户 `200000429462`,`threeDSecure:false`。
- **CardToken 支付**:`paySceneParams` 用 `cardToken` + `cvv`(免卡号),商户 `200000429066`。
- **ApplePay/设备支付**(UAT `200000088041`):`type:DEVICE_PAY`、`devicePayType:APPLE_PAY`(可 GOOGLE_PAY/SAMSUNG_PAY)、`cardNum`/`cardExpYear`/`cardExpMonth`(加密)、`cryptoFmt:3DSECURE`、`payCrypt`(加密)、`eci:07`。
- **DCC**(UAT `200000091394`/`200000091441`):顶层带 `currencyConversion`(dccAmount/exchangeRate/markupRate/dccQuoteId/dccUptake=`ACCEPTED`);先查 DCC Qualification 再 Create。
- **PayFacs 子商户**(`200000433782`):顶层带 `payFacsSubMerchant`(identifier/tradingName/registeredName/bankIndustryCode/marketplaceId 等)。

### AFT 测试卡(DIRECTPAY / AFT 用)
| 卡号 | 有效期 | CVV | Bank | Brand | 类型 | 国家 |
| --- | --- | --- | --- | --- | --- | --- |
| `4229989999000012` | 31/12 | 871 | MYBK | VISA | CC | MY→AE |
| `4123709999000029` | 31/12 | 855 | ZABK | VISA | DC | ZA |
| `4761349999000039` | 31/12 | 998 | SGBK | VISA | CC | US |

## AUTODEBIT(协议代扣)
```json
"paySceneCode": "AUTODEBIT",
"paySceneParams": { "authProtocolNo": "2520250424112248107256",
  "oneTimePayment": "", "redirectUrl": "http://www.example.com" }
```
- `authProtocolNo` = `deduct.t_deduct_protocol.deduct_protocol_no`(需先签约成功)。签约链路与库表见 [[scn_online_business_auto_debit]]。

## JSAPI(PayBy 内嵌 H5 商城)
```json
"paySceneCode": "JSAPI", "paySceneParams": { "oneTimePayment": "" }
```

## PAYANDSIGN(支付并签约)
```json
"paySceneCode": "PAYANDSIGN",
"paySceneParams": { "protocolSceneCode": "120", "oneTimePayment": "" }
```
- `protocolSceneCode` = 自动扣款服务 ID(配置读取规则)。常量 `120`,SIM 测试 `111`;配置表 `deduct.t_deduct_protocol_config.protocol_scene_code`。详见 [[scn_online_business_auto_debit]]。

## PREAUTH / CAPTURE / PREAUTHVOID(预授权 → 请款 / 撤销)
**PREAUTH**(SIM `200000435288`;支持卡 / CardToken / 设备支付,参数同 DIRECTPAY):
```json
"paySceneCode": "PREAUTH",
"paySceneParams": { "cardNo": "加密|5123450000000008", "holderName": "加密|FANGYONG LIU",
  "expYear": "39", "expMonth": "01", "cvv": "加密|100", "platformType": "WEB",
  "customerId": "987654321", "realIP": "222.64.177.132", "saveCard": "false",
  "redirectUrl": "https://www.example.com" }
```
**CAPTURE**(对已 PREAUTH 订单请款):
```json
"paySceneCode": "CAPTURE",
"paySceneParams": { "preauthOrderNo": "131762264194063167", "oneTimePayment": "" }
```
**PREAUTHVOID(Void,撤销预授权)**:
```json
"paySceneCode": "PREAUTHVOID",
"paySceneParams": { "preauthOrderNo": "131762266616069566", "oneTimePayment": "" }
```
预授权全流程见 [[scn_online_business_pre_auth]]。

## QA 关注点
- 每个 `paySceneCode` 的 `paySceneParams` **必填项**差异是核心负例来源(缺 authCode/appId/redirectUrl/preauthOrderNo 等)。
- DIRECTPAY 三态:首次卡 / CardToken / 设备支付(ApplePay);`saveCard=true` 首次支付返回 `cardToken` 供后续复用。
- AFT / DCC / PayFacs 是 DIRECTPAY/PAYPAGE 的**顶层扩展块**(accountFundingParameter / currencyConversion / payFacsSubMerchant),与 paySceneParams 并列。
- 加密字段务必走 SDK 加密;测试卡结果由卡号/有效期触发(见测试卡 Reference)。
