---
id: scn_mit_cit_directpay_subsequent
object_type: Scenario
domain: authorization-protocol
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: confluence:AQ/2095087700
tags:
- CIT
- DirectPay
- MPGS
- tokenized
subdomain: mit-cit
module: test-guide
sensitivity: normal
name: DirectPay 后续CIT测试场景
aliases: []
related_services: []
related_tables:
- acquireii.t_card_info
- member.tr_bank_account
related_scenarios:
- scn_mit_cit_directpay_first
- scn_mit_autodebit
related_logs: []
related_requirements: []
related_failures: []
---

## 触发/入口
通过 Create Order API 创建 `paySceneCode=DIRECTPAY` 订单，使用 `cardToken` + `agreementInfo` + `source=INTERNET` 发起后续 CIT。

## 前置条件
- 已完成 DirectPay 首次 CIT（参见 [[scn_mit_cit_directpay_first]]），获得可用的 `cardToken`。
- ACS 配置：MerchantId=测试 mid，paramKey=`DEDUCT_INTERNAL_PARTNER`，paramValue=`Y`。
- 商户已开通产品：Auto Debit、Direct Pay Domestic Card、Direct Pay INTL Card。
- 获取 cardToken 方式：
  - `select card_token from acquireii.t_card_info where global_id=131768567354074283;`
  - `select OUT_ACCOUNT_TOKEN from member.tr_bank_account where MEMBER_ID={mid} and STATUS=1 order by create_time desc;`

## 操作步骤
调用 Create Order API，payload：
```
{
  "merchantOrderNo": "M$random12",
  "subject": "acquire2.0 bate",
  "totalAmount": { "currency": "AED", "amount": 100.00 },
  "paySceneCode": "DIRECTPAY",
  "paySceneParams": {
    "cardToken": "11189567742463674064",
    "cvv": "加密|100",
    "customerId": "99999000000",
    "email": "",
    "platformType": "WEB",
    "threeDSecure": "true",
    "realIP": "222.64.177.132",
    "redirectUrl": "https://www.qianwen.com/",
    "source": "INTERNET",
    "agreementVersion": "V1",
    "agreementSign": "True",
    "protocolNotifyUrl": "https://www.qianwen.com"
  },
  "deviceId": "",
  "secondaryMerchantId": "",
  "notifyUrl": "https://www.qianwen.com/",
  "agreementInfo": {
    "agreementType": "RECURRING",
    "numberOfPayments": 1,
    "amountVariability": "VARIABLE",
    "expiryDate": "2035-01-01",
    "paymentFrequency": "DAILY",
    "minimumDaysBetweenPayments": 1
  }
}
```

## DB 校验点
- `select * from deduct.t_deduct_protocol where partner_id=200000054800 and status="A" order by create_time desc;` —— 获取 `deduct_protocol_no` 用于后续 MIT。
- `select * from member.tr_bank_card_token where institution_code='MPGS' and status='Y' order by create_time desc;` —— 校验 token 状态。
- 通过 `acquireii.t_card_info.card_token` 与 `member.tr_bank_account.OUT_ACCOUNT_TOKEN` 取得 cardToken。

## 预期结果
- CIT 成功，路由到 MPGS 通道。
- `t_deduct_protocol` 中产生新数据，`status='Y'`。
- 发往 MPGS 的请求中包含 `agreement` 字段（含 `id`、`type=RECURRING`、`expiryDate`、`paymentFrequency`、`numberOfPayments`、`amountVariability`、`minimumDaysBetweenPayments`），`transaction.source=INTERNET`，`sourceOfFunds.provided.card.storedOnFile=TO_BE_STORED`。
