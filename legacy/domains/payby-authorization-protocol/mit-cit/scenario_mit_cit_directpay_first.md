---
id: scn_mit_cit_directpay_first
object_type: Scenario
domain: authorization-protocol
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: confluence:AQ/2095087700
tags:
- CIT
- DirectPay
- MPGS
- 3DS
- 首次签约
subdomain: mit-cit
module: test-scenario
sensitivity: normal
name: DirectPay 首次CIT测试场景
aliases: []
related_services: []
related_tables:
- deduct.t_deduct_protocol
- member.tr_bank_card_token
related_scenarios:
- scn_mit_cit_payandsign
- scn_mit_cit_directpay_subsequent
- scn_mit_autodebit
related_logs: []
related_requirements: []
related_failures: []
---

## 触发/入口
通过 Create Order API 创建一笔 `paySceneCode = DIRECTPAY` 的订单，并携带 `agreementInfo`，触发首次 CIT 走 MPGS 渠道完成签约。

## 前置条件
- ACS 配置：`MerchantId=你的测试 mid`，`paramKey=DEDUCT_INTERNAL_PARTNER`，`paramValue=Y`
- 商户开通产品：
  - Auto Debit
  - Direct Pay Domestic Card
  - Direct Pay INTL Card

## 操作步骤
通过 Create Order API 创建一笔 "DirectPay" 订单，请求体需包含：
- 卡信息（FPN/DPN）：`cardNo`、`holderName`、`cvv`、`expYear`、`expMonth`
- 商户客户号：`customerId`
- 签约相关参数：`saveCard=true`、`agreementVersion=V1`、`agreementSign=True`、`protocolNotifyUrl`
- `threeDSecure=true`、`source=INTERNET`、`platformType=WEB`
- `agreementInfo`：`agreementType=RECURRING`、`numberOfPayments=1`、`amountVariability=VARIABLE`、`expiryDate=2035-01-01`、`paymentFrequency=DAILY`、`minimumDaysBetweenPayments=1`

示例 payload：
```json
{
  "merchantOrderNo": "M$random12",
  "subject": "acquire2.0 bate",
  "totalAmount": { "currency": "AED", "amount": 100.00 },
  "paySceneCode": "DIRECTPAY",
  "paySceneParams": {
    "cardNo": "加密|5123450000000008",
    "holderName": "加密|tanyijian",
    "cvv": "加密|100",
    "expYear": "39",
    "expMonth": "01",
    "platformType": "WEB",
    "threeDSecure": "true",
    "customerId": "99999000000",
    "realIP": "222.64.177.132",
    "saveCard": "true",
    "redirectUrl": "https://www.qianwen.com/",
    "source": "INTERNET",
    "agreementVersion": "V1",
    "agreementSign": "True",
    "protocolNotifyUrl": "https://www.qianwen.com"
  },
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

需满足的条件：
- 触发 3DS 校验
- 路由到 MPGS 渠道
- CIT 成功后获取 `deduct_protocol_no`，用于后续 MIT 交易

## DB 校验点
- 获取 `deduct_protocol_no`：
  ```
  select * from deduct.t_deduct_protocol where partner_id=200000054800 and status="A" order by create_time desc;
  ```
  CIT 成功后，该表会新增一条数据，`status = 'Y'`。
- 校验 MPGS token 是否生成：
  ```
  select * from member.tr_bank_card_token where institution_code='MPGS' and status='Y' order by create_time desc;
  ```

## 预期结果
- 触发 3DS 校验并完成验证
- 路由到 MPGS 渠道
- CIT 成功，`deduct.t_deduct_protocol` 新增数据 `status='Y'`，`member.tr_bank_card_token` 生成 `institution_code='MPGS'`、`status='Y'` 记录
- 日志中可观察到 `BankClientImpl` 向 MPGS 发送的请求，`agreement` 字段被正确携带（含 `expiryDate`、`numberOfPayments`、`amountVariability`、`minimumDaysBetweenPayments`、`id`、`paymentFrequency`、`type=RECURRING`），`sourceOfFunds.provided.card.storedOnFile=TO_BE_STORED`，`apiOperation=PAY`
- 拿到的 `deduct_protocol_no` 可用于后续 MIT（AutoDebit）交易
