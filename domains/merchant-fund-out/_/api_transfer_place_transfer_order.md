---
id: api_transfer_place_transfer_order
object_type: API
domain: merchant-fund-out
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: wiki:d24969b4-625e-4ea0-b20d-669043b3a083
tags:
- transfer
- fund-out
subdomain: null
module: null
sensitivity: normal
name: 出款到账户接口
aliases:
- transfer/placeTransferOrder
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
商户出款到账户场景的下单接口，支持以账户标识（如手机号）作为收款方进行出款。

产品集：Transfer to bank、Transfer To Bank Via SWIFT（通过 swift 网络出款）、Transfer To Bank Via FEDWIRE（通过 fedwire 网络出款）

## 路径/方法
SGS: `transfer/placeTransferOrder`

接口文档: https://developers.payby.com/docs/Transfer/

## 入参
重要参数：

```
{
  "amount": {
    "currency": "AED",
    "amount": 500
  },
  "beneficiaryIdentity": "加密|+971-585920614",
  "beneficiaryIdentityType": "PHONE_NO"
}
```

- `amount.currency`：出款币种（如 AED）
- `amount.amount`：出款金额
- `beneficiaryIdentity`：收款方标识（加密），示例为手机号
- `beneficiaryIdentityType`：收款方标识类型，示例为 `PHONE_NO`

## 出参
原文未提供。

## 错误码
原文未提供。

## 测试校验点
- 校验下单成功后落库 `mhtfundout.t_fundout_account_order`
- 校验 `beneficiaryIdentity` 加密传输
- 校验 `beneficiaryIdentityType=PHONE_NO` 场景下能正常受理
- 校验产品集（Transfer to bank / SWIFT / FEDWIRE）路由到对应出款网络
- 校验商户控台展示出款到账户订单
