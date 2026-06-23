---
id: api_kyc_passport_verify_again
object_type: API
domain: kyc
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: confluence:PMDPayment/1446215797
tags:
- passport
- kyc
- ocr
subdomain: passport_kyc
module: active-account
sensitivity: normal
name: 重新验证KYC接口
aliases:
- Verify again
- verify-again
related_services:
- svc_kyc
related_tables: []
related_scenarios: []
---

## 用途
当 passport OCR 信息细节不正确时，用户可调用该接口重新发起一次新的 KYC journey。

## 关联关系
- **所属服务**:[[svc_kyc]](related_services;api→service 边)
- **读写的表**:待补
- **被哪些场景测**:§9 登录/KYC 回归(待补具体 scenario 对象)

## 路径/方法
- 路径：`/kyc/active-account/v1/passport/main/verify-again`
- Method：POST

## 入参
Request body：

| Paramters | Data Type | Mandatory | Example | Description |
|---|---|---|---|---|
| token | String | Y | 75762b77ed11445abd6078f739b53be7 | flow id |

## 出参
status=200 为成功

Response body：

| Paramters | Data Type | Mandatory | Example | Description |
|---|---|---|---|---|
| commandType | String | Y | moveForward | tips: show tips；moveForward: go to the next step |
| commandData | json | Y | TipsInfo | 1, commandType=tips 返回 TipsInfo；2, commandType=moveForward 获取下一步 |

commandData 示例（start signzy kyc journey）：
```json
{
  "commandType" : "moveForward",
  "commandData" : {
    "nextStep": "/kyc/home"
  }
}
```

## 错误码
原文未列出专属错误码。

## 测试校验点
- 入参 token 为必填，应为有效的 kyc flow id。
- status=200 视为成功。
- 校验响应 commandType 取值仅为 `tips` 或 `moveForward`。
- 当 commandType=moveForward 时，commandData.nextStep 应返回 `/kyc/home`，引导用户进入新的 KYC journey。
- 当 commandType=tips 时，commandData 应为 TipsInfo 结构。
- 仅适用于 OCR 护照信息有误场景下用户主动重新验证。
