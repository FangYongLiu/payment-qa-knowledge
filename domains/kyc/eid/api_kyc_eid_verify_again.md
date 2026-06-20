---
id: api_kyc_eid_verify_again
object_type: API
domain: kyc
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: confluence:PMDPayment/1089405294
tags:
- EID
- KYC
- journey
subdomain: eid
module: main
sensitivity: normal
name: 重新验证接口
aliases:
- Verify again
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
当 EID OCR 信息不正确时，用户可以发起重新验证，启动一次新的 KYC journey。

## 路径/方法
- API: `/kyc/active-account/v1/eid/main/verify-again`
- Method: POST

## 入参
Request body:

| Paramter | Data Type | Mandatory | Example | Description |
|---|---|---|---|---|
| token | String | Y | 75762b77ed11445abd6078f739b53be7 | flow id |

## 出参
status=200 为成功

Response body:

| Paramter | Data Type | Mandatory | Example | Description |
|---|---|---|---|---|
| commandType | String | Y | moveForward | tips: show tips；moveForward: go to the next step；action |
| commandData | json | Y | TipsInfo | 1. commandType=tips, return TipsInfo；2. commandType=moveForward, get next step |

commandData 示例：

1. start signzy kyc journey
```
{
  "commandType" : "moveForward",
  "commandData" : {
    "nextStep": "/kyc/home"
  }
}
```

## 错误码
原文未提供。

## 测试校验点
- token 为必填，使用当前 KYC flow 的 token 调用。
- OCR 信息错误场景下触发，response 应返回 commandType=moveForward，nextStep 指向 `/kyc/home`，启动新的 journey。
- status=200 视为成功。
- 校验对 commandType=tips 与 commandType=moveForward 两类返回的处理分支。
