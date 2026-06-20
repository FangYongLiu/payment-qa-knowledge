---
id: api_kyc_eid_verify_again
object_type: API
domain: kyc
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: wiki:c77c6bdf-23d4-4c31-b325-128a8f8a6d3e
tags:
- EID
- KYC
- journey
subdomain: eid
module: main
sensitivity: normal
name: 重新验证接口 (verify-again)
aliases:
- verify-again
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
当 EID OCR 信息不正确时，用户可以选择重新验证（verify again），由该接口启动一个新的 KYC journey。

## 路径/方法
- 路径：`/kyc/active-account/v1/eid/main/verify-again`
- Method：POST

## 入参
Request body：

| 参数 | 类型 | 必填 | 示例 | 描述 |
|---|---|---|---|---|
| token | String | Y | 75762b77ed11445abd6078f739b53be7 | flow id |

## 出参
status=200 为成功。

Response body：

| 参数 | 类型 | 必填 | 示例 | 描述 |
|---|---|---|---|---|
| commandType | String | Y | moveForward | tips: show tips；moveForward: go to the next step；action |
| commandData | json | Y | TipsInfo | 1. commandType=tips 返回 TipsInfo；2. commandType=moveForward 进入下一步 |

commandData 示例（启动 signzy kyc journey）：

```json
{
  "commandType" : "moveForward",
  "commandData" : {
    "nextStep": "/kyc/home"
  }
}
```

## 错误码
原文未列出该接口的具体错误码。

## 测试校验点
- 入参 `token` 必传，需为有效的 KYC flow id。
- 仅在 EID OCR 信息不正确（details incorrect）的场景下被调用，调用后应启动新的 journey。
- 成功响应 status=200，返回 `commandType=moveForward`，`commandData.nextStep` 指向 `/kyc/home`，由前端跳转到新的 KYC 入口。
- 当返回 `commandType=tips` 时，需按 TipsInfo 结构展示提示。
- 与 `start-journey`、`get-result` 流程的衔接：verify-again 后用户重新走 EID journey，再通过 get-result 获取结果。
