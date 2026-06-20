---
title: BotIM Token刷新流程
domain: payby-core-systems
kind: wiki_page
slug: botim-token-refresh-flow
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:0eb622de-7e30-4c72-9fce-f6ecec6f59d6
tags: []
---

# BotIM Token刷新流程

本页描述 BotIM 客户端发起 Token 刷新时，经 sgs-grpc、personal、pts 的服务调用链路，以及刷新失败时的重登录与 Token 保存处理。

## 参与方

- user：发起刷新的终端用户
- botim：BotIM 客户端
- sgs-grpc：网关层服务
- personal：个人账户服务
- pts：Token 颁发服务

## 调用链路

按顺序触发的消息：

1. user → botim：`Refresh token`
2. botim → sgs-grpc：调用 `/personal/v1/refresh-token`
3. sgs-grpc → personal：`Refresh token`
4. personal → pts：`Refresh token`
5. pts → personal：返回结果
6. personal → sgs-grpc：返回结果
7. sgs-grpc → botim：返回结果

## 失败处理（Refresh Failed）

- 当 refresh-token 调用失败时，进入 `Refresh Failed` 分支：
  - botim 执行 `Re-login`（自身调用，重新登录获取新 Token）

## Token 保存与响应

- botim 执行 `Save token`（自身调用，保存新 Token）
- botim → user：`Response`，将刷新结果返回用户

## 视觉约定

- 实线箭头：请求
- 虚线箭头：响应
- `Refresh Failed` 框仅在刷新失败时进入 Re-login 步骤
