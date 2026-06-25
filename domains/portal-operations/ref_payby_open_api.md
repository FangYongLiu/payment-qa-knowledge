---
id: ref_payby_open_api
object_type: reference
name: PayBy 对外开放接口参考(场景码/返回码/数据结构)
aliases: [payby open api, pay scene code, return codes, api data structures, product catalog]
domain: portal-operations
status: active
owner: fangyong.liu@astratech.ae
reviewer: yijian.tan
last_reviewed_at: '2026-06-25'
source_type: upload
source_ref: 'api-docs/payby-api-v2.25'
tags: [payby-api, payscene, return-code, data-structure, integration]
related_services: [svc_merchant]
---

# PayBy 对外开放接口参考(场景码/返回码/数据结构)

> PayBy 商户对外接口(v2.25)的支付场景码、返回码、订单/通用数据结构与产品类型参考。供对接联调与故障定位。下单接口字段对象「待补」(原文引用 `api_payby_payment_create_order`，尚未建对象)。

## 交易场景码(paySceneCode)
| paySceneCode | 说明 |
| --- | --- |
| JSAPI | JSAPI 支付 |
| INAPP | App 支付 |
| PAYPAGE | 支付网页支付 |
| DYNQR | 动态码支付 |
| QRPAY | 付款码支付 |
| AUTODEBIT | 协议授权支付 |
| CASHTOPUP | 现金充值支付 |
| FACE | 人脸支付 |
| DIRECTPAY | 直联支付 |
| EWALLET | 电子钱包支付 |
| PAYANDSIGN | PAYANDSIGN |
| PREAUTH | 预授权 |
| PREAUTHVOID | 预授权取消(未 capture 才可 void) |
| CAPTURE | 预授权确认 |

各场景 `paySceneParams` / `interactionParams` 要点:
- **JSAPI/PAYPAGE/DYNQR/EWALLET/PAYANDSIGN/CASHTOPUP** 返回 `tokenUrl`(有效期 1 小时，过期需相同业务参数重建订单)。
- **QRPAY**:`authCode`(必填);**AUTODEBIT**:`authProtocolNo`(必填);**INAPP**:`iapDeviceId`+`appId`(必填)。
- **FACE**:`authToken`+`uniqueDevice`(必填)。
- **DIRECTPAY/PREAUTH**:按首次支付 / savedCard / 分期 / devicePay 子模式区分卡参数(`cardNo/holderName/cvv/expYear/expMonth/platformType/customerId/realIP/redirectUrl` 等，加密传输);interactionParams `threeDSecureDom`，分期含 `installmentUrl`。
- **PREAUTHVOID/CAPTURE**:`preauthOrderNo`(必填)。
- 通用:`oneTimePayment`(true 时仅允许支付一次，失败置失败)、`threeDSecure`(PayBy 风控判断优先于商户要求)、`customerId`(商户侧唯一标识，用于静默开户，单次支付也需上报)。

## 产品类型清单
| 产品 | 说明 |
| --- | --- |
| Basic Payment Gateway | JSAPI/APP/PAYPAGE/DYNQR 等线上 |
| InApp | InApp 应用内支付 |
| Smart Purchase | 智能 POS/小白盒等设备收款 |
| QRPay | 扫码枪扫用户付款码 |
| Transfer | 转账到 PayBy 账户 |
| Transfer to bank | 转账到银行卡 |
| Auto Debit | 授权协议号代扣 |
| Cash Top Up | 现金完成线上订单支付 |

## 通用响应头(ResponseHeader)
| 字段 | 类型 | 描述 |
| --- | --- | --- |
| applyStatus | String(16) | SUCCESS / FAIL / ERROR |
| code | String(10) | 返回码 |
| msg | String(200) | 返回信息 |

## 返回码总览

### 系统级
| code | msg | 原因 | 解决 |
| --- | --- | --- | --- |
| 0 | SUCCESS | 成功 | — |
| 400 | INVALID_PARAMETER | 参数错误 | 调整参数 |
| 400 | REQUESTTIME_TOO_EARLY / TOO_LATER | 请求时间偏差过大 | 调整请求时间 |
| 402 | RATE_LIMIT_REJECT | 请求过于频繁 | 降低频率 |
| 403 | UNAUTHORIZED | API 未授权 | 联系 PayBy |
| 404 | SERVICE_NOT_AVAILABLE | 服务不可用 | 联系 PayBy |
| 500 | SYSTEM_ERROR | 系统错误 | 稍后重试 |
| 504 | SERVICE_TIMEOUT | 服务超时 | 稍后重试 |
| 601 | RISK_FAIL | 风控校验失败 | 调整业务 |

### 订单与状态(62001-62041)
ORDER_PAID(62001)/ORDER_FAILURE(62002)/ORDER_SETTLED(62003)/MERCHANT_ORDER_NO_NOT_EXIST(62004)/REFUND_AMOUNT_EXCEEDED(62006，可退=原额−已退−退款中)/REFUND_MERCHANT_ORDER_NO_NOT_EXIST(62007)/EXPIREDTIME 校验(62008/62009)/PAYSCENECODE_ILLEGAL(62012)/ORDER_NOT_PAID(62015)/MERCHANT_ORDER_NO_EXIST(62016)/REFUND_MERCHANT_ORDER_NO_EXIST(62017)/ORDER_SUCCESS(62028)/ORDER_CREATED(62029)/ORDER_BANK_FAIL(62030)/ORDER_NO_NOT_EXIST(62035)/ACQUIRE_ORDER_REVOKED(62040)/ACQUIRE_ORDER_REFUNDED(62041)。

### 收付双方/会员
PAYERMID_NOT_EXIST(62018)/PAYEEMID_NOT_EXIST(62019)/PAYERMID_PAYEEMID_ARE_SAME(62020)/NAME_NOT_MATCH(62023)/BENEFICIARY_NOT_EXIST(62027)/INVALID_PAYEEMID(62086)。

### 退款/冲正/产品配置
PRODUCT_IS_NOT_APPLIED(62026)/INVALID_SECONDARY_MERCHANT(62038)/REVOKE_FAILURE(62039)/REFUND_REJECTED(62045)/REVOKE_REJECTED(62046)/SHARING_MEMBER_NOT_EXIST(62083)/REFUND_SHARING_MEMBER_MISMATCH(62084)。

### 对账单/设备
STATEMENT_NOT_EXIST(62013)/STATEMENT_NOT_GENERATED(62014，10 点后再下载);MISSING_DEVICE_ID/APP_ID/AUTHCODE(62031-62033)/INVALID_APP_ID(62034)。

## 订单数据结构要点

### 商户订单号约定
- 仅字母/数字/`-`/`_`，商户自定义、保持唯一(建议时间+随机序列)。
- 重发支付用原订单号;已支付/已取消的订单号不能重发。

### AcquireOrder(收单订单)关键字段
`requestTime`、`merchantOrderNo`(64)、`orderNo`(32)、`status`(AcquireOrderStatus)、`paymentInfo`、`product`、`totalAmount`(Money)、`payeeMid`、`expiredTime`、`notifyUrl`、`subject`、`paySceneCode`、`paySceneParams`、`deviceId`、`secondaryMerchantId`、`failCode`/`failDes`、`revoked`(=true 判定冲正成功)、`sharingInfoList`、`promotionInfoList`、`subjectAr`、`accountFundingParameter`(AFT 交易，PAYPAGE/INAPP/AUTODEBIT/DIRECTPAY/PAYANDSIGN 时必传)、`payFacsSubMerchant`。

### PaymentInfo / ChannelParam / CardInfo
- PaymentInfo:`paidAmount`、`paidTime`、`payerMid`、`payerFeeAmount`、`payeeFeeAmount`、`payChannel`(如 `BALANCE-余额`)、`settlementAmount`、`cardInfo`、`channelParam`。
- ChannelParam.extension(JSON):`AuthCode`、`RRN`、`Stan`、`AcquireCode`、`AcquireMessage`，例 `{"AuthCode":"245408","Stan":"245408","AcquireCode":"00","AcquireMessage":"Approved","RRN":"529512245408"}`。
- CardInfo:`brand`(MASTERCARD/VISA/AE/DISCOVER/JCB)、`last4`、`cardType`(DC 借记/CC 贷记)、`expMonth/expYear`、`cardToken`、`issueCountry`、`issueBank`。
- Money:`amount` Decimal(12,2)、`currency`(如 AED)。
- AccessoryContent:AmountDetail(discountableAmount/amount/vatAmount/tipAmount)、GoodsDetail(body/categoriesTree/goodsCategory/goodsId/goodsName)、TerminalDetail。

### 通用结构(查询/对账单/分账/拒付/VAM/AFT)
- OrderIndexRequest:`merchantOrderNo` 与 `orderNo` 二选一(不可同空/同有)。
- UpdateExpiredTimeRequest:增 `expiredTime`。
- GetStatementRequest:`statementDate`(如 `20200120`)。
- SharingInfo:`sharingIdentityMid`、`sharingAmount`、`sharingIdentitySeqId`(从 1 连号不可重复)、`sharingMemo`、可选结算金额/手续费/`withholdAndRemitFee`。
- AcquireChargeback(拒付):chargebackTime/merchantOrderNo/orderNo/payAmount/chargebackAmount/caseType/partnerId。
- VamDepositOrder:transactionTime/orderNo/amount/status(如 SUCCESS)/referenceNo/remitterInfo/senderBankCode/depositDetails/collectIBAN。
- AccountFundingParameter:`purpose`(CRYPTOCURRENCY_PURCHASE/MERCHANT_SETTLEMENT/OTHER/PAYROLL)、senderType、sender(SenderData)、recipient(RecipientData);RecipientAccount.identifierType(BANK_ACCOUNT_IBAN/CARD_NUMBER 等)。
- 订单尾部补充:`payerFeeAmount`、`arrivalTime`(预计到账时间)。

## 接口文档变更记录
| 版本 | 日期 | 主要变更 |
| --- | --- | --- |
| v2.19 | 2024-06-27 | 创建订单新增 `subjectAr` |
| v2.20 | 2024-08-07 | 新增拒付通知 |
| v2.21 | 2024-09-18 | 新增 VAM 充值通知 |
| v2.22 | 2025-03-18 | 新增微信小程序支付 |
| v2.23 | 2025-04-15 | 新增 AFT 参数 |
| v2.24 | 2025-05-20 | DIRECTPAY 支持 DevicePay |
| v2.25 | 2025-10-23 | 新增预授权;查询/通知返回 AuthCode/RRN/Stan/AcquireCode/AcquireMessage |

> 部分数据结构(GoodsDetail/TerminalDetail/PayFacsSubMerchant 等)在原文为分页表，完整字段以官方 v2.25 接口文档为准;下单接口对象「待补」。
