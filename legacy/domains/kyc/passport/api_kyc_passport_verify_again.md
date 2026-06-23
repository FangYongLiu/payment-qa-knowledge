---
id: api_kyc_passport_verify_again
object_type: API
domain: kyc
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: wiki:e75788c0-8dcd-4b0c-95e3-8c08067ad9e7
tags:
- passport
- kyc
- journey
subdomain: passport
module: active-account
sensitivity: normal
name: 重新验证接口
aliases:
- Verify again
- verify-again
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
当 Passport OCR 信息不正确时，用户可以选择重新验证，发起一段新的 KYC journey。

## 路径/方法
- API：`/kyc/active-account/v1/passport/main/verify-again`
- Method：POST

## 入参
Request body：

| Parameter | Data Type | Mandatory | Example | Description |
|---|---|---|---|---|
| token | String | Y | 75762b77ed11445abd6078f739b53be7 | flow id |

## 出参
status=200 为成功

Response body：

| Parameter | Data Type | Mandatory | Example | Description |
|---|---|---|---|---|
| commandType | String | Y | moveForward | tips: show tips；moveForward: go to the next step |
| commandData | json | Y | TipsInfo | 1, commandType = tips, return TipsInfo；2, commandType = moveForward, get next step |

commandData 示例：

1、start signzy kyc journey
```json
{
  "commandType": "moveForward",
  "commandData": {
    "nextStep": "/kyc/home"
  }
}
```

## 错误码
原文未列出。

## 测试校验点
- 入参 token 必传，且为有效的 KYC flow id。
- 仅在 OCR 信息不正确场景下调用，调用后会发起一段新的 journey。
- 校验响应 status=200 视为成功。
- 校验 commandType=moveForward 时，commandData.nextStep 返回 `/kyc/home`，前端可据此跳转重新发起 journey。
- 校验 commandType=tips 时，正确解析并展示 TipsInfo。
