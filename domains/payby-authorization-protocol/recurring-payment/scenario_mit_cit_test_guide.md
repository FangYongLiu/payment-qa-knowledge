---
id: scn_mit_cit_test_guide
object_type: Scenario
domain: payby-authorization-protocol
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: wiki:8d7a8617-1740-4670-8898-b035d5fdf23c
tags:
- MIT
- CIT
- MPGS
- test
subdomain: recurring-payment
module: test-guide
sensitivity: normal
name: MIT/CIT MPGS 测试场景集
aliases: []
related_services: []
related_tables:
- deduct.t_deduct_protocol
- member.tr_bank_card_token
- acquireii.t_card_info
- member.tr_bank_account
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 触发/入口
- payandsign CIT：调用 SGS API `/acquire2/placeOrder`，paySceneCode=`PAYANDSIGN`
- directpay 1st CIT：通过 Create Order API，paySceneCode=`DIRECTPAY`，携带卡信息（FPN/DPN）+ agreementInfo + customerId
- directpay Subsequent CIT：通过 Create Order API，paySceneCode=`DIRECTPAY`，source=`INTERNET`，使用 agreement id + cardToken
- Auto Debit MIT：通过 Create Order API，paySceneCode=`AUTODEBIT`，source=`MERCHANT`，使用 authProtocolNo

## 前置条件
1. 在 acs 增加配置：
   - MerchantId: 测试 mid
   - paramKey: `DEDUCT_INTERNAL_PARTNER`
   - paramValue: `Y`
2. 开通产品：
   - Auto Debit
   - Direct Pay Domestic Card
   - Direct Pay INTL Card

## 操作步骤

### 1) payandsign CIT
请求 SGS `/acquire2/placeOrder`：
```
"paySceneCode": "PAYANDSIGN",
"paySceneParams": {
  "protocolSceneCode": "111",
  "oneTimePayment": ""
}
```
进入 paypage 通过 payby/botim app 支付，需满足：
- 触发 3DS 验证
- 在 payby/botim app 内完成卡支付
- 路由到 cko/mpgs 渠道

### 2) directpay 1st CIT
通过 Create Order API 创建 DirectPay 订单，payload 关键字段：
- paySceneCode=`DIRECTPAY`
- paySceneParams：cardNo、holderName、cvv、expYear/expMonth、threeDSecure=`true`、customerId、saveCard=`true`、source=`INTERNET`、agreementVersion=`V1`、agreementSign=`True`、protocolNotifyUrl
- agreementInfo：agreementType=`RECURRING`、numberOfPayments、amountVariability=`VARIABLE`、expiryDate、paymentFrequency=`DAILY`、minimumDaysBetweenPayments

需满足：
- 触发 3DS 验证
- 路由到 mpgs 渠道

### 3) directpay Subsequent CIT
通过 Create Order API 创建 DirectPay 订单，paySceneParams 使用：
- cardToken（从 `acquireii.t_card_info.card_token` 或 `member.tr_bank_account.OUT_ACCOUNT_TOKEN` 获取）
- cvv、customerId、threeDSecure=`true`、source=`INTERNET`、agreementVersion=`V1`、agreementSign=`True`
- 同样携带 agreementInfo

### 4) Auto Debit MIT
通过 Create Order API 创建 AutoDebit 订单：
```
"paySceneCode": "AUTODEBIT",
"paySceneParams": {
  "authProtocolNo": "611752565230002944",
  "source": "MERCHANT",
  "agreementVersion": "V1"
}
```

## DB 校验点
- 获取 deduct_protocol_no（用于后续 MIT）：
  ```sql
  select * from deduct.t_deduct_protocol where partner_id=200000054800 and status="A" order by create_time desc;
  ```
  CIT 成功后会新增数据且 status=`Y`；CKO 渠道多次 CIT 成功时旧数据 status 置为 `F`；MPGS 渠道多次 CIT 成功则会持续生成新数据。
- 验证 MPGS 卡 token：
  ```sql
  select * from member.tr_bank_card_token where institution_code='MPGS' and status='Y' order by create_time desc;
  ```
- 获取 cardToken：
  ```sql
  select card_token from acquireii.t_card_info where global_id=131768567354074283;
  select OUT_ACCOUNT_TOKEN from member.tr_bank_account where MEMBER_ID={mid} and STATUS=1 order by create_time desc;
  ```

## 预期结果
- CIT 成功后 `t_deduct_protocol` 生成新数据，status=`Y`
- `tr_bank_card_token` 中 institution_code=`MPGS` 且 status=`Y` 的记录存在
- 日志中向 MPGS 渠道发送的请求包含 `agreement` 字段，例：
  ```
  bankClient.put.url:https://mtf.gateway.mastercard.com/api/rest/version/100/merchant/TEST461000000011/order/.../transaction/...
  request:{"agreement":{"expiryDate":"2035-01-01","numberOfPayments":1,"amountVariability":"VARIABLE","minimumDaysBetweenPayments":1,"id":"131768385854019414","paymentFrequency":"DAILY","type":"RECURRING"},"apiOperation":"PAY","sourceOfFunds":{"provided":{"card":{...,"storedOnFile":"TO_BE_STORED"}},"type":"CARD"},"transaction":{"source":"INTERNET"},"order":{...},"authentication":{"transactionId":"..."}}
  ```
- 拿到 deduct_protocol_no 后即可发起 MIT 交易
