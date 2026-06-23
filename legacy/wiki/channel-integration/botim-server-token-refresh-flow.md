---
title: BOTIM服务端Token刷新流程
domain: channel-integration
kind: wiki_page
slug: botim-server-token-refresh-flow
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:e6841f36-24d4-4fcc-9708-5a7164389d09
tags: []
---

# BOTIM服务端Token刷新流程

本页描述 BOTIM 服务端通过 `sgs-grpc` 代理向 `personal` 与 `pts` 完成 token 刷新的端到端时序，并覆盖刷新失败时的重登录分支。

## 参与方

- **user**：发起刷新请求的用户端
- **botim**：BOTIM 服务端，负责代理转发与本地 token 存储
- **sgs-grpc**：grpc 代理层
- **personal**：个人服务，负责调用底层 token 颁发服务
- **pts**：底层 token 颁发服务

## 成功路径时序

1. `Refresh token`：user → botim
2. `/personal/v1/refresh-token`：botim → sgs-grpc
3. `Refresh token`：sgs-grpc → personal
4. `Refresh token`：personal → pts
5. `New token`：pts → personal（返回）
6. `New token`：personal → sgs-grpc（返回）
7. `New token`：sgs-grpc → botim（返回）
8. `Save token`：botim 本地保存新 token
9. `Response`：botim → user（返回）

## 刷新失败分支（Refresh Failed）

- 当 botim 收到的刷新结果判定为失败时，进入 `Refresh Failed` 分支。
- botim 触发 `Re-login`（自调用），走重登录流程替代继续使用旧/新 token。

## 关键约定

- botim 对外暴露刷新入口，对内统一通过 `sgs-grpc` 调用 `/personal/v1/refresh-token`。
- 新 token 由 `pts` 实际颁发，经 `personal` → `sgs-grpc` → `botim` 逐层回传。
- 仅在拿到有效 New token 时执行 `Save token`，再响应 user。
