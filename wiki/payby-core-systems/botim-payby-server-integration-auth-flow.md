---
title: BOTIM-PayBy服务端集成首次认证登录流程
domain: payby-core-systems
kind: wiki_page
slug: botim-payby-server-integration-auth-flow
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:5b1644df-997f-479d-8160-f0b57c5a9f5b
tags: []
---

# BOTIM-PayBy服务端集成首次认证登录流程

本页描述 BOTIM 作为客户端网关，通过 `sgs-grpc` 调用 PayBy 后端完成用户首次绑定与登录的端到端时序。

## 参与方

- **user**：终端用户（actor）
- **botim**：客户端网关
- **sgs-grpc**：对外 gRPC 接入层
- **personal**：个人账户域服务
- **pts**：Token 服务
- **member**：会员服务
- **protocol**：协议签署服务

## 入口与绑定检查

1. **Use Wallet**：user 自调用，发起使用钱包动作。
2. **Check bind PayBy or not**：user → botim，检查是否已绑定 PayBy。
   - 2.1：botim → user，返回检查结果。

## First Authentication（首次认证）

该阶段包裹在 `First Authentication` frame 中：

3. **Show PayBy protocol page**：user 自调用，展示 PayBy 协议页。
4. **Login and sign protocol**：user → botim，登录并签署协议。

### 绑定客户 `/personal/v1/bind-customer`

- 4.1：botim → sgs-grpc，调用 `/personal/v1/bind-customer`。
  - 4.1.1：sgs-grpc → personal，**Bind customer**。
    - 4.1.1.1：personal → member，**Register or update customer**。
    - 4.1.1.2：member → personal，返回。
    - 4.1.1.3：personal → protocol，**Sign protocols**。
    - 4.1.1.4：protocol → personal，返回。
  - 4.1.2：personal → sgs-grpc，返回。
- 4.2：sgs-grpc → botim，返回 **Member ID**。

## 登录与 Token 下发

`First Authentication` frame 结束后，继续登录流程：

### 登录 `/personal/v1/login`

- 4.3：botim → sgs-grpc，调用 `/personal/v1/login`。
  - 4.3.1：sgs-grpc → personal，**Login**。
    - 4.3.1.1：personal → pts，**Apple token**。
    - 4.3.1.2：pts → personal，返回 **Access token**。
  - 4.3.2：personal → sgs-grpc，返回 **Access token**。
- 4.4：sgs-grpc → botim，返回 **Access token**。

### Token 持久化与回传

- 4.5：botim 自调用，**Save token or anything**。
- 4.6：botim → user，返回 **Botim token**。

## 关键调用关系

- botim 作为客户端网关，统一通过 `sgs-grpc` 暴露的两个接口完成绑定与登录：
  - `/personal/v1/bind-customer`
  - `/personal/v1/login`
- sgs-grpc 将请求路由至 personal 域；personal 进一步协调 member（注册/更新）、protocol（协议签署）与 pts（Token 颁发）。
- 首次流程产出两类关键标识：**Member ID**（绑定阶段）与 **Access token**（登录阶段），最终由 botim 转换为 **Botim token** 下发给 user。
