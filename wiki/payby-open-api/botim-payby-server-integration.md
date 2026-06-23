---
title: BOTIM接入PayBy服务端集成流程
domain: payby-open-api
kind: wiki_page
slug: botim-payby-server-integration
status: active
owner: relink
reviewer: UNREVIEWED
source_type: relink
source_ref: relink:payby-open-api
---

# BOTIM接入PayBy服务端集成流程

本页描述 BOTIM 服务端接入 PayBy 钱包的整体时序，分为「首次认证（绑定客户并签约协议）」与「登录获取 Access Token」两个阶段。涉及的服务端组件包括 `botim`、`sgs-grpc`、`personal`、`pts`、`member`、`protocol`。

## 参与方

- **user**：终端用户
- **botim**：BOTIM 业务后端
- **sgs-grpc**：对外网关层（PayBy open-api 入口）
- **personal**：个人账户/客户域服务
- **pts**：Token 颁发服务
- **member**：会员注册/更新服务
- **protocol**：协议签约服务

## 入口流程

用户进入钱包时，BOTIM 先判断该用户是否已绑定 PayBy：

1. `Use Wallet`：user → botim
2. `Check bind PayBy or not`：user → botim
   - 2.1 botim 返回结果给 user

依据是否绑定，进入「首次认证」或直接进入「登录」。

## 首次认证（First Authentication）

用于尚未绑定 PayBy 的用户，完成客户绑定与协议签约。

3. `Show PayBy protocol page`：展示 PayBy 协议页
4. `Login and sign protocol`：user → botim，用户登录并同意签约
5. `4.1 /personal/v1/bind-customer`：botim → sgs-grpc [[api_personal_bind_customer]]
   - `4.1.1 Bind customer`：sgs-grpc → personal
     - `4.1.1.1 Register or update customer`：personal → member
     - `4.1.1.2` member → personal 返回
     - `4.1.1.3 Sign protocols`：personal → protocol
     - `4.1.1.4` protocol → personal 返回
   - `4.1.2` personal → sgs-grpc 返回
6. `4.2 Member ID`：sgs-grpc → botim 返回 Member ID

> 该阶段的产物为 **Member ID**，用于后续登录换取 Access Token。

## 登录获取 Access Token

首次认证完成后（或用户已绑定时）继续走登录流程：

- `4.3 /personal/v1/login`：botim → sgs-grpc [[api_personal_v3_auth_login]]
  - `4.3.1 Login`：sgs-grpc → personal
    - `4.3.1.1 Apple token`：personal → pts
    - `4.3.1.2 Access token`：pts → personal
  - `4.3.2 Access token`：personal → sgs-grpc
- `4.4 Access token`：sgs-grpc → botim
- `4.5 Save token or anything`：botim 本地保存 token 等信息
- `4.6 Botim token`：botim → user，下发 BOTIM 侧 token

## 接口一览

| 接口 | 调用方 → 被调方 | 作用 |
| --- | --- | --- |
| `/personal/v1/bind-customer` | botim → sgs-grpc | 绑定客户、注册/更新会员、签约协议 |
| `/personal/v1/login` | botim → sgs-grpc | 登录并换取 Access Token |

## 备注

- 请求使用实线箭头，响应使用虚线箭头。
- 业务域：`payby-open-api`，由 `sgs-grpc` 作为统一入口。
- Apple token 由 `personal` 向 `pts` 申请，最终由 `pts` 颁发 Access Token。
