---
id: api_kyc_confirm_change_mobile
object_type: API
domain: kyc
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: wiki:2654d3b2-24d5-481b-926b-96f41f946ae8
tags:
- CGS
- EID
- change-mobile
- KYC
subdomain: active-account
module: eid
sensitivity: normal
name: KYC 确认换绑手机号接口 (confirm-change-mobile)
aliases:
- confirm-change-mobile
related_services: []
related_tables: []
related_scenarios:
- kyc-change-mobile-flow
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
EID KYC 换绑手机号流程的最终确认接口（CGS API v2）。用户在前序步骤完成 EID 验证、选择需换绑的会员账号、密码校验后，调用本接口提交 token 与 id，由后端完成换绑动作并返回展示指令（tips/moveForward），用于驱动前端展示成功/挂起/失败/异常等结果页或进入下一步。

## 路径/方法
- Path：`/kyc/active-account/v1/eid/main/confirm-change-mobile`
- 类型：CGS API（Eid kyc cgs api v2）

## 入参
Request body：

| Parameter | Data Type | Mandatory | Sample | Description |
|---|---|---|---|---|
| token | String | Y | 2344551223234455 | Kyc flow token |
| id | String | Y | 1223234455 | A hash value |

## 出参
Response body：

| Parameter | Data Type | Mandatory | Sample | Description |
|---|---|---|---|---|
| commandType | String | Y | tips | tips: show tips info；moveForward: go to the next step；action: Need to respond to business matters |
| commandData | TipsInfo (json) | Y | 见下方各场景示例 | 当 commandType=tips 时返回 TipsInfo；当 commandType=moveForward 时为下一步的 commandData |

TipsInfo 常见字段：`tipImg`、`tipText`、`title`、`type`(Page/Dialog)、`pageCode`、`redirectView[]`(`viewName`/`viewAction.actionCode`/`viewType`/`viewUrl`)。

各业务场景返回示例：

1) Change Mobile Success
```json
{
  "commandType": "tips",
  "commandData": {
    "tipImg": "https://alioss.payby.com/cms/4b149102_new_success.png",
    "tipText": "Your account is now active.",
    "title": "You're all set!",
    "type": "Page",
    "pageCode": "kycSuccess"
  }
}
```

2) Change Mobile Pending
```json
{
  "commandType": "tips",
  "commandData": {
    "tipImg": "https://alioss.payby.com/cms/d537f674_new_pending.png",
    "tipText": "It may take up to 48 hours to verify your account. We’ll notify you as soon as it’s ready.",
    "title": "We are verifying your account",
    "type": "Page",
    "pageCode": "kycPending",
    "redirectView": [
      {"viewName": "Okay", "viewAction": {"actionCode": "close_mini_program"}, "viewType": "primary"}
    ]
  }
}
```

3) Change Mobile Failed
```json
{
  "commandType": "tips",
  "commandData": {
    "tipImg": "https://alioss.payby.com/cms/aaea7fdb_new_failed.png",
    "tipText": "You can try again or contact our support team for help.",
    "title": "We couldn’t verify your account",
    "type": "Page",
    "pageCode": "kycFail",
    "redirectView": [
      {"viewName": "Try again", "viewAction": {"actionCode": "navigation"}, "viewType": "primary", "viewUrl": "/kyc/home"},
      {"viewName": "Contact us", "viewAction": {"actionCode": "navigation"}, "viewType": "default", "viewUrl": "https://botim.me/oa/chat?oaid=IDVTFY5"}
    ]
  }
}
```

4) Change Mobile Exception
```json
{
  "commandType": "tips",
  "commandData": {
    "tipText": "Your account couldn’t be linked to your mobile number. Check your connection and try again.",
    "title": "Account connection failed",
    "type": "Dialog",
    "pageCode": "chgMobExp",
    "redirectView": [
      {"viewName": "Try again", "viewAction": {"actionCode": "navigation"}, "viewType": "primary", "viewUrl": "/kyc/choose-account"}
    ]
  }
}
```

5) Common Verification Exception
```json
{
  "commandType": "tips",
  "commandData": {
    "tipText": "Information verification failed. Please try again later.",
    "type": "Dialog",
    "redirectView": [
      {"viewName": "OK", "viewType": "default"}
    ]
  }
}
```

## 错误码
原文未单独列出错误码列表；异常以 `commandType=tips` + `type=Dialog` 的 TipsInfo 返回（如 `pageCode=chgMobExp` 的 Change Mobile Exception 与 Common Verification Exception）。

## 测试校验点
- token、id 必传校验，缺失或非法时应触发 Common Verification Exception 类提示。
- commandType 仅取值 `tips` / `moveForward` / `action`；当为 `tips` 时 commandData 为 TipsInfo；当为 `moveForward` 时进入下一步流程。
- Success 场景：返回 `pageCode=kycSuccess`、`type=Page`、对应成功图与文案。
- Pending 场景：返回 `pageCode=kycPending`，包含 redirectView `Okay` -> `actionCode=close_mini_program`。
- Failed 场景：返回 `pageCode=kycFail`，包含 `Try again`(跳 `/kyc/home`) 与 `Contact us`(跳 botim 链接) 两个 redirectView。
- Change Mobile Exception：`type=Dialog`、`pageCode=chgMobExp`，`Try again` 跳 `/kyc/choose-account`。
- Common Verification Exception：`type=Dialog`，单按钮 `OK`，无 viewUrl。
- 与下游 Dubbo 联动校验：成功路径应触发 `IMemberIdentityFacade#changeMobileAndRefreshKyc`（scene=`changeMobile`），并基于 `IMemberFacade#queryEidBoundAccount` 选定的 originalMemberId/newMemberId 完成换绑。
- TipsInfo 字段（tipImg/tipText/title/type/pageCode/redirectView）原样返回，不应被改写。
