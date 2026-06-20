---
title: BOTIM钱包绑定与认证时序流程
domain: payby-core-systems
kind: wiki_page
slug: botim-wallet-binding-auth-flow
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:00ee9166-336e-44bf-9e4b-e170fd8e95cb
tags: []
---

# BOTIM钱包绑定与认证时序流程

本页描述用户在 BOTIM 中使用 PayBy 钱包时，从检测绑定状态、首次签约协议、到登录获取 token 的完整端到端时序交互。

## 参与方（Lifelines）

按时序图从左至右：

- **user**：终端用户（actor）
- **botim**：客户端网关
- **sgs-grpc**：gRPC 聚合服务
- **personal**：个人域服务
- **pts**：token 服务
- **member**：会员域服务
- **protocol**：协议域服务

## 总体交互链路

- botim 作为客户端网关，统一调用 sgs-grpc
- sgs-grpc 向下游 personal 委派业务处理
- personal 进一步与 member、protocol、pts 协作完成注册、签约与发 token

## 入口：检测绑定状态

1. **Use Wallet**：user 在 botim 上触发使用钱包
2. **Check bind PayBy or not**：user → botim 检查是否已绑定 PayBy
   - 2.1：botim → user 返回检查结果

## First Authentication（首次认证）

该 frame 包含步骤 3 ~ 4.2，用于首次绑定客户与签署协议。

- **3. Show PayBy protocol page**：user 侧展示 PayBy 协议页
- **4. Login and sign protocol**：user → botim 提交登录并签署协议
- **4.1 `/personal/v1/bind-customer`**：botim → sgs-grpc
  - **4.1.1 Bind customer**：sgs-grpc → personal
    - 4.1.1.1 **Register or update customer**：personal → member
    - 4.1.1.2 member → personal 返回结果
    - 4.1.1.3 **Sign protocols**：personal → protocol
    - 4.1.1.4 protocol → personal 返回结果
  - 4.1.2 personal → sgs-grpc 返回结果
- **4.2 Member ID**：sgs-grpc → botim 返回会员 ID

## 登录与 Token 交换

完成首次认证 frame 之后继续执行：

- **4.3 `/personal/v1/login-or-refresh`**：botim → sgs-grpc
  - **4.3.1 Login**：sgs-grpc → personal
    - 4.3.1.1 **Apple token**：personal → pts
    - 4.3.1.2 **Access token**：pts → personal
  - 4.3.2 **Access token**：personal → sgs-grpc
- **4.4 Access token**：sgs-grpc → botim
- **4.5 Save token or anything**：botim 本地保存 token 等信息
- **4.6 Botim token**：botim → user 返回 botim 侧 token

## 关键接口

- `/personal/v1/bind-customer`：绑定客户（注册/更新会员 + 签署协议）
- `/personal/v1/login-or-refresh`：登录或刷新，换取 Access token
