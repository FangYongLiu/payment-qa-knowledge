---
id: scn_mit_autodebit
object_type: Scenario
domain: payby-authorization-protocol
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: confluence:AQ/2095087700
tags:
- MIT
- AutoDebit
- MPGS
subdomain: null
module: null
sensitivity: normal
name: AutoDebit MIT 代扣测试场景
aliases: []
related_services: []
related_tables: []
related_scenarios:
- scn_mit_cit_payandsign
- scn_mit_cit_directpay_first
- scn_mit_cit_directpay_subsequent
related_logs: []
related_requirements: []
related_failures: []
---

## 触发/入口
通过 Create Order API 创建 `paySceneCode=AUTODEBIT` 的 AutoDebit 订单，发起 MIT(商户发起)代扣交易。

## 前置条件
- 已通过 CIT(payandsign / directpay 1st / directpay Subsequent)成功签约，获取到可用的 `authProtocolNo`(即 deduct_protocol_no)。
- ACS 配置已就绪：MerchantId 为测试 mid，paramKey=`DEDUCT_INTERNAL_PARTNER`，paramValue=`Y`。
- 已开通产品：Auto Debit、Direct Pay Domestic Card、Direct Pay INTL Card。
- 协议数据校验：
  - `select * from deduct.t_deduct_protocol where partner_id=200000054800 and status="A" order by create_time desc;` 中存在对应协议且 status='Y'。
  - `select * from member.tr_bank_card_token where institution_code='MPGS' and status='Y' order by create_time desc;` 中存在对应的 MPGS card token。

## 操作步骤
调用 Create Order API，使用 `source=MERCHANT` 与 `authProtocolNo`(agreement id)发起 AutoDebit 订单，示例 paySceneParams：

```
"paySceneCode": "AUTODEBIT",
"paySceneParams": {
  "authProtocolNo": "611752565230002944",
  "source": "MERCHANT",
  "agreementVersion": "V1"
}
```

## DB 校验点
- `deduct.t_deduct_protocol`：传入的 `authProtocolNo` 对应记录 status='Y'(协议有效)。
- `member.tr_bank_card_token`：`institution_code='MPGS'` 且 status='Y' 的 token 可用于 MIT 代扣。

## 预期结果
- 使用已签约的 `authProtocolNo` 以 MERCHANT 来源成功发起 AutoDebit MIT 代扣订单。
- 后续交易通过 MPGS 通道完成，无需再次 3DS 认证。
