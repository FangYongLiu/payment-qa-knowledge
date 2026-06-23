---
id: api_kyc_body_unauth_apply
object_type: API
domain: kyc
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: wiki:c77c6bdf-23d4-4c31-b325-128a8f8a6d3e
tags:
- kyc
- liveness
- unauth
subdomain: body-auth
module: liveness
sensitivity: normal
name: 未认证活体核身申请接口 (body-unauth apply)
aliases:
- body-unauth apply
- 未认证活体核身申请
related_services:
- svc_kyc
---

## 用途
为未登录/未认证场景下的业务功能提供安全保障，基于手机号申请活体核身（liveness verify），生成视频采集验证入口。与已认证场景的 `/kyc/body-auth/v1/liveness/apply` 区别在于：未认证用户需在请求中显式传入 `mobile`（密文）。

## 路径/方法
- API：`/kyc/body-unauth/v1/liveness/apply`
- Method：POST

## 入参
Request body：

| 名称 | 类型 | 非空 | 示例 | 描述 |
|---|---|---|---|---|
| mobile | String | Y | - | mobile no.（Ciphertext） |
| ticket | String | Y | 75762b77ed11445abd6078f739b53be7 | Unique ticket for body verification, cache key |
| redirectUrl | String | N | - | when the user complete the kyc flow, then redirect to Botim page |

## 出参
Response：

| 名称 | 类型 | 非空 | 示例 | 描述 |
|---|---|---|---|---|
| model | String | Y | HTTP | verify method，SDK(Yitu SDK)、HTTP(Webview video url) |
| videoUrl | String | Y | https://xxxx.xx/?url=https://liveliness-preproduction.signzy.app/consumer/3e458b68-9777-4b2d-b9f0-d6056e83acc4/token/xxnmAFSkliaBf91z36Ux | HTTP：MP address + signzy url（小程序地址由 xukunlong 提供），该地址需要后端做 encodeUrl 操作；SDK：router://xxx.xx（该地址由 native 提供 liubin） |

## 错误码
原文未列出本接口专属错误码。

## 测试校验点
1. `mobile` 必须以密文形式传入，明文传入应被拒绝。
2. `ticket` 必填，作为 body 验证的唯一凭据/缓存 key，重复或缺失场景需校验。
3. `redirectUrl` 选填，传入时完成 kyc flow 后应能跳回 Botim 页面。
4. 响应 `model=HTTP` 时，`videoUrl` 应为 MP 地址 + signzy url 的拼接形式，且 signzy url 部分已做 encodeUrl 处理。
5. 响应 `model=SDK` 时，`videoUrl` 应为 native 提供的 `router://` 路由地址。
6. 与已认证接口 `/kyc/body-auth/v1/liveness/apply` 对比：未认证接口必须额外携带 `mobile`，缺失 `mobile` 应返回失败。
7. 校验未认证用户场景下能正常拿到 signzy 视频采集 URL 并完成跳转。
