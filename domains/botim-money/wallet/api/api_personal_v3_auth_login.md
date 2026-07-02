---
id: api_personal_v3_auth_login
object_type: API
domain: wallet
status: active
owner: qianlong.wang
reviewer: qianlong.wang
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: wiki:a01637cc-4974-45c3-b1e9-d194dac7ed1f
tags:
- login
- auth
- access-token
subdomain: personal
module: auth
sensitivity: normal
name: 客户登录接口(v3)
aliases:
- /personal/v3/auth/login
- Customer Login
related_services:
- svc_personal
---

## 用途
- 客户端登录 PayBy 的统一入口，合并原有 `/personal/apply/authToken` 与 `/personal/v2/auth/login` 两个接口
- 登录成功后向客户端返回 access token
- 属于 Login for Customer 流程中的 Step 1.2.1 新增 API

## 路径/方法
- API Code: `/personal/v3/auth/login`
- API Name: Customer Login
- 所属系统: personal
- 文档参考: http://sim.intra.test2pay.com/api-doc/sgs-api/personal-sgs-api/
- 相关参考: Personal - Member Onboarding

## 入参
原文未在本接口下单独列出入参字段。该接口由原 `/personal/apply/authToken` 与 `/personal/v2/auth/login` 合并而来。

## 出参
- Access Token（登录成功后返回给客户端）

## 错误码
原文未列出。

## 测试校验点
- 验证 `/personal/v3/auth/login` 调用后返回 access token 给客户端
- 验证该接口能够覆盖原 `/personal/apply/authToken` 与 `/personal/v2/auth/login` 的合并能力（无需再分两步调用）
- 与 server-end Login（基于 Member ID + Botim UID 返回 Access Token）的能力衔接验证
- 客户登录前置条件：Bind Customer 流程已完成（member 与 Botim UID 已建立绑定）
