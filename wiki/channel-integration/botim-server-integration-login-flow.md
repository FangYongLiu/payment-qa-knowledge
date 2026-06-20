---
title: Botim服务端集成 - 登录与PayBy认证流程
domain: channel-integration
kind: wiki_page
slug: botim-server-integration-login-flow
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:5fc1a54a-07c2-4842-b881-a2150e7a27e1
tags: []
---

# Botim服务端集成 - 登录与PayBy认证流程

本页描述用户在 Botim 登录时，Botim 服务端与 PayBy 侧（sgs-grpc、pts、member）之间的交互时序：首次登录需先完成绑定（First Authentication），后续登录走标准 PayBy Login 并返回 Botim token。

## 参与方

- **user**：终端用户
- **botim**：Botim 服务端
- **sgs-grpc**：PayBy 对接网关
- **pts**：PayBy 内部服务
- **member**：会员服务

## 总体时序

1. `Login botim`：user → botim 发起登录
2. **首次登录**：执行 First Authentication（绑定流程），获取 Member ID
3. **后续登录**：调用 Login PayBy 完成认证
4. `Botim token`：botim 将 token 返回给 user

## First Authentication（仅首次登录）

该分组框仅在初次登录时触发，用于在 PayBy 侧建立或更新客户并完成绑定：

- 1.1 `Call bind api`：botim → sgs-grpc
- 1.1.1 `Bind`：sgs-grpc → pts
- 1.1.1.1 `Create or update customer`：pts → member
- 1.1.1.2 返回 `Member ID`：member ⇢ pts
- 1.1.2 返回 `Member ID`：pts ⇢ sgs-grpc
- 1.2 返回 `Member ID`：sgs-grpc ⇢ botim

完成后，botim 持有该用户对应的 `Member ID`。

## PayBy 登录（每次登录均执行）

绑定完成或已存在绑定关系后，进入标准登录流程：

- 1.3 `Login PayBy`：botim → sgs-grpc
- 1.3.1 `Login`：sgs-grpc → pts
- 1.3.2 pts ⇢ sgs-grpc 返回（登录结果）
- 1.4 sgs-grpc ⇢ botim 返回（登录结果）
- 1.5 `Botim token`：botim ⇢ user

## 关键说明

- 首次登录 = First Authentication（1.1–1.2） + PayBy 登录（1.3–1.5）
- 非首次登录 = 仅 PayBy 登录（1.3–1.5）
- 绑定步骤通过 `Create or update customer` 在 member 侧建立会员档案，并将 `Member ID` 逐层回传至 botim
- 最终用户拿到的是 Botim token，而非 PayBy 内部凭证
