---
id: api_kyc_passport_confirm_info
object_type: API
domain: kyc
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: wiki:e75788c0-8dcd-4b0c-95e3-8c08067ad9e7
tags:
- passport
- kyc
- confirm
subdomain: active-account
module: passport
sensitivity: normal
name: 确认Passport信息接口
aliases:
- confirm-info
related_services:
- svc_kyc
---

## 用途
用户确认OCR识别出的护照信息（用户不可修改）。该接口提交后**不会进入人工审核流程**。通常在 `get-result` 返回 `commandType=action` 且携带 `passportInfo` 后调用，由用户点击确认触发。

## 路径/方法
- Path: `/kyc/active-account/v1/passport/main/confirm-info`
- Method: `POST`
- Domain:
  - SIM: `https://sim.test2pay.com/cgs/api`
  - UAT / PROD: 见总览

## 入参
Request body (JSON)：

| 参数 | 类型 | 必填 | 示例 | 说明 |
|------|------|------|------|------|
| token | String | Y | 75762b77ed11445abd6078f739b53be7 | kyc flow id |

## 出参
Response body (JSON)：

| 参数 | 类型 | 必填 | 示例 | 说明 |
|------|------|------|------|------|
| commandType | String | Y | tips | `tips`: show tips；`moveForward`: go to the next step |
| commandData | json | Y | TipsInfo 结构 | 当 commandType=tips 返回 TipsInfo；当 commandType=moveForward 返回下一步 action |

### 典型返回示例

1) kyc fail (commandType=tips)
```json
{
  "commandType":"tips",
  "commandData": {
    "type": "Page",
    "title": "Kyc fail",
    "tipText": "Kyc fail, please retry",
    "tipImg": "https://sim-m.test2pay.com/xxxxx/logo.png"
  }
}
```

2) kyc process (commandType=tips)
```json
{
  "commandType":"tips",
  "commandData": {
    "type": "Page",
    "title": "Kyc complete",
    "tipText": "We are verifying your account",
    "tipImg": "https://sim-m.test2pay.com/xxxxx/logo.png"
  }
}
```

3) kyc success (commandType=moveForward)
```json
{
  "commandType":"moveForward",
  "commandData": {
    "type": "Popup",
    "title": "Kyc success",
    "tipText": "Your account has actived.",
    "tipContent": "You need to upload your Emirates lD copy before Nov. 15,2023 to continue using your account",
    "tipImg": "https://sim-m.test2pay.com/xxxxx/logo.png"
  }
}
```

## 错误码
原文未单独列出业务错误码；接口语义通过 HTTP `status=200` 与响应体 `commandType` (`tips` / `moveForward`) 进行业务结果区分。

## 测试校验点
1. 入参 `token` 必传，缺失或非法 token 应被拒绝。
2. 调用成功后**不进入人工审核流程**，需校验后端审核任务表/流程未生成对应人工审核记录。
3. 用户**不能修改** passportInfo，确认接口本身仅依赖 token，不接受 passport 字段入参。
4. 三种业务分支返回结构正确：
   - kyc fail → `commandType=tips`，type=Page，title="Kyc fail"。
   - kyc process → `commandType=tips`，title="Kyc complete"，tipText="We are verifying your account"。
   - kyc success → `commandType=moveForward`，type=Popup，title="Kyc success"，包含 `tipContent` 提示后续上传 Emirates ID。
5. 同一 token 重复确认的幂等性（不应重复变更状态）。
6. 上游 [[api_kyc_passport_get_result]] 返回 `commandType=action` 且含 `passportInfo` 时，前端才允许调用本接口。
7. 与 [[api_kyc_passport_verify_again]]（信息有误时）互斥：用户确认后不应再允许 verify-again。
8. 响应 `tipImg` 等 URL 字段格式校验。
