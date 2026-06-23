---
id: api_kyc_eid_confirm_change_mobile
object_type: API
domain: kyc
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: confluence:PMDPayment/1751384142
tags:
- eid
- change-mobile
- cgs
- confirm
subdomain: active-account
module: eid
sensitivity: normal
name: EID Change Mobile 确认接口
aliases: []
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
EID KYC 流程中确认换绑手机的 CGS 接口（v2）。根据后端处理结果，返回 `commandType=tips` 展示页面/弹窗信息，或返回 `commandType=moveForward` 指示前端进入下一步。

## 路径/方法
- 路径：`/kyc/active-account/v1/eid/main/confirm-change-mobile`
- 类型：CGS API

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
| commandType | String | Y | tips | `tips`：展示 tips 信息；`moveForward`：进入下一步；`action`：需要响应业务事件 |
| commandData | TipsInfo（json） | Y | 见下方示例 | 当 `commandType=tips` 时返回 TipsInfo；当 `commandType=moveForward` 时返回 next step 的 commandData |

### commandData 场景示例

1) Change Mobile Success（type=Page, pageCode=kycSuccess）
```
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

2) Change Mobile Pending（type=Page, pageCode=kycPending，redirectView: Okay → close_mini_program）
```
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

3) Change Mobile Failed（type=Page, pageCode=kycFail，redirectView: Try again → /kyc/home；Contact us → BOTIM 客服链接）
```
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

4) Change Mobile Exception（type=Dialog, pageCode=chgMobExp，redirectView: Try again → /kyc/choose-account）
```
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

5) Common Verification Exception（type=Dialog，无 pageCode；redirectView: OK）
```
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
原文未列出错误码；异常路径通过 `commandType=tips` + 不同 `pageCode`/`type` 体现：
- `kycFail`（Page）— Change Mobile Failed
- `chgMobExp`（Dialog）— Change Mobile Exception
- 无 pageCode（Dialog）— Common Verification Exception

## 测试校验点
- 入参 `token`、`id` 均必填，缺失应被拒绝。
- 成功场景：`commandType=tips`，`commandData.type=Page`，`pageCode=kycSuccess`，文案/图片与示例一致。
- Pending 场景：`pageCode=kycPending`，含按钮 Okay，`actionCode=close_mini_program`。
- Failed 场景：`pageCode=kycFail`，含 Try again（跳转 `/kyc/home`）与 Contact us（跳转 `https://botim.me/oa/chat?oaid=IDVTFY5`）两个 redirectView。
- Exception 场景：`type=Dialog`，`pageCode=chgMobExp`，Try again 跳转 `/kyc/choose-account`。
- Common Verification Exception：`type=Dialog`，仅一个 OK 按钮，`viewType=default`。
- `commandType=moveForward` 时应返回下一步所需的 `commandData`，前端据此跳转下一步。
- 校验与下游 Dubbo 接口的联动：换绑确认前应能正确查询 EID 绑定账户（参见 [[api_member_query_eid_bound_account]]），确认后调用换绑并刷新 KYC（参见 [[api_member_change_mobile_refresh_kyc]]，`scene=changeMobile`）。
