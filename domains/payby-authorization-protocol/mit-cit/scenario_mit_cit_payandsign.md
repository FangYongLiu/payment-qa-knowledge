---
id: scn_mit_cit_payandsign
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
- PayAndSign
- MPGS
- 3DS
subdomain: mit-cit
module: null
sensitivity: normal
name: PayAndSign CIT 签约支付测试场景
aliases: []
related_services: []
related_tables:
- deduct.t_deduct_protocol
- member.tr_bank_card_token
related_scenarios:
- scn_mit_cit_directpay_first
- scn_mit_cit_directpay_subsequent
- scn_mit_autodebit
related_logs: []
related_requirements: []
related_failures: []
---

## 触发/入口
- 调用 SGS API：`/acquire2/placeOrder`
- 关键参数：
  - `paySceneCode = PAYANDSIGN`
  - `paySceneParams.protocolSceneCode = 111`
  - `paySceneParams.oneTimePayment = ""`

## 前置条件
- 在 acs 上为测试 MID 添加配置：
  - `MerchantId`: 测试 mid
  - `paramKey = DEDUCT_INTERNAL_PARTNER`
  - `paramValue = Y`
- 商户开通产品：
  - Auto Debit
  - Direct Pay Domestic Card
  - Direct Pay INTL Card

## 操作步骤
1. 通过 `/acquire2/placeOrder` 创建 PAYANDSIGN 订单。
2. 进入 paypage，使用 payby/botim app 完成支付，需满足：
   - 触发 3DS 验证
   - 在 payby/botim app 内完成卡支付
   - 路由到 cko/mpgs 通道
3. CIT 成功后，获取 `deduct_protocol_no`，用于后续 MIT 交易。

## DB 校验点
- 协议表：
  ```sql
  select * from deduct.t_deduct_protocol
  where partner_id=200000054800 and status="A"
  order by create_time desc;
  ```
  - CIT 成功后会生成一条新数据，`status = 'Y'`
  - 若在 CKO 通道多次 CIT 成功，旧数据 status 会被置为 `F`
  - 若在 MPGS 通道多次 CIT 成功，会生成新数据
- 卡 token 表：
  ```sql
  select * from member.tr_bank_card_token
  where institution_code='MPGS' and status='Y'
  order by create_time desc;
  ```

## 预期结果
- CIT 交易成功，可获取 `deduct_protocol_no`。
- `deduct.t_deduct_protocol` 新增记录，`status = 'Y'`。
- `member.tr_bank_card_token` 中存在 `institution_code='MPGS'`、`status='Y'` 的记录。
- 日志中可见发往 MPGS 的请求包含 `agreement` 字段，例如：
  - `bankClient.put.url: https://mtf.gateway.mastercard.com/api/rest/version/100/merchant/TEST461000000011/order/.../transaction/...`
  - request 含 `"agreement":{"expiryDate":"2035-01-01","numberOfPayments":1,"amountVariability":"VARIABLE","minimumDaysBetweenPayments":1,"id":"131768385854019414","paymentFrequency":"DAILY","type":"RECURRING"}`
  - `"sourceOfFunds.provided.card.storedOnFile":"TO_BE_STORED"`
  - `"apiOperation":"PAY"`，`"transaction.source":"INTERNET"`
