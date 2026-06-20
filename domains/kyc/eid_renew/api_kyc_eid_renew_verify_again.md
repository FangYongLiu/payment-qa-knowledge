---
id: api_kyc_eid_renew_verify_again
object_type: API
domain: kyc
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: wiki:af2b7970-1661-4d20-90f7-3b86b8f72d58
tags:
- eid
- renew
- kyc
subdomain: eid_renew
module: null
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
当 EID OCR 识别出的信息不正确时，用户可通过该接口重新发起一次新的 renew journey。

## 路径/方法
- API: `/kyc/active-account/v1/eid/renew/verify-again`
- Method: POST

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

1、start signzy renew journey
```
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
- token 必填，缺失或非法时应被拒绝。
- 仅在 OCR 信息不正确的场景下允许调用，触发后应能启动一个新的 renew journey。
- 成功响应 status=200，commandType=moveForward 时，commandData.nextStep 返回 `/kyc/home`。
- 校验返回结构与 commandType / commandData 的对应关系（tips 返回 TipsInfo，moveForward 返回下一步动作）。
