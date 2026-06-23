---
title: Botim-PayBy服务端集成方案总览
domain: channel-integration
kind: wiki_page
slug: botim-payby-server-integration-overview
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:PMDPayment/1072791687
tags: []
---

# Botim-PayBy服务端集成方案总览

本页概述 Botim 4.0 与 PayBy 之间服务端集成的目标、两大业务场景（绑定客户、登录），以及涉及的系统协作要点。

## 集成目标

- 实现 gRPC 网关
- 实现客户信息交换（exchange customer information）
- 实现服务端登录（server-end login）与刷新 Token
- 兼容此前 PayBy 调用 Botim 的既有 API（参考 [[botim-payby-outbound-apis]]）

## 业务范式

集成围绕两个核心范式展开：

1. **Bind Customer**：Botim 客户进入 4.0 钱包功能时，由 Botim 调用 PayBy 完成会员的创建/绑定/UID 替换。
2. **Login for Customer**：客户在客户端通过新的统一接口完成登录并取得 Access Token。

### Bind Customer 场景

触发与展示规则：

- **触发时机**：客户使用钱包相关功能时（System: botim）
- **协议页展示时机**：客户首次使用 4.0 钱包

`personal` 域 `4.1.1 Bind customer` 行为分支：

- **Create new member**：开通 AED BASIC 账户，签署 basic account 协议与 TOU
- **Bind with exist member**：将 4.0 Botim UID 与已存在的 member 关联，签署 basic account 协议与 TOU
- **Replace Botim UID**（3.0 升级到 4.0）：解除 3.0 Botim UID 关联，关联 4.0 Botim UID

入参（M=Mandatory，O=Optional）：

- Mobile Number - M
- Botim UID - M
- Client IP - M
- Botim Old UID（可为 3.0 UID）- O

返回：Member ID - M

按 Mobile Number 分支处理（Bind customer by mobile number）：

| Scenario | Action |
|---|---|
| Same Mobile、UID existed | idempotent，返回已存在的 member |
| Mobile not exist PayBy member | Create member |
| Mobile exist PayBy member but no Botim UID associated | Bind with exist member |
| Mobile exist Botim UID 且与 Botim Old UID 相同（仅 3.0→4.0） | Replace Botim UID |
| Mobile exist Botim UID 且与 Botim Old UID 不同 | Not allow to do anything |

`member` 域支持以 Old UID 替换 member 的 UID，并支持把 UID 绑定到 member：

- Replace UID 入参：Member ID - M, Old Botim UID - M, New Botim UID - M
- Bind UID to Member 入参：Member ID - M, Botim UID - M

`personal` 域 `4.3.1 Login`（服务端登录）：

- 入参：Member ID - M, Botim UID - M
- 返回：Access Token - M

详见接口文档 [[api_personal_bind_customer]]。

### Login for Customer 场景

- **1.2.1**：新增 `/personal/v3/auth/login`
- 该接口合并原 `/personal/apply/authToken` 与 `/personal/v2/auth/login`，向客户端返回 Access Token
- 系统：personal
- 参考：Personal - Member Onboarding

详见 [[api_personal_v3_auth_login]] 与 [[api_personal_login_or_refresh]]。

## 系统交互角色

涉及的系统域：

- **botim**：触发绑定，处理钱包入口与协议页展示
- **personal**：bind-customer、login-or-refresh、v3 auth login 等对外 API
- **member**：member 的创建/UID 绑定/UID 替换

## 网关与协议

- 采用 gRPC 网关传输，复用 sgs http protocol
- 协议结构（DownstreamCaller、DFRequest/DFResponse、ApplicationMessage）与字段定义见 [[botim-payby-grpc-gateway-protocol]]
- 报文加解密（AES-256，AES/GCM/NoPadding，IV 拼接在密文前，Base64 编码）见 [[botim-payby-payload-security]]

## API 清单

Personal Documentation：`http://sim.intra.test2pay.com/api-doc/sgs-api/personal-sgs-api/`

| API Code | API Name |
|---|---|
| `/personal/v1/bind-customer` | Bind Customer（[[api_personal_bind_customer]]） |
| `/personal/v1/login-or-refresh` | Login or Refresh Token（[[api_personal_login_or_refresh]]） |
| `/personal/v3/auth/login` | Customer Login（[[api_personal_v3_auth_login]]） |

PayBy 反向调用 Botim 的 outbound 接口集合详见 [[botim-payby-outbound-apis]]。

## 影响点

- Botim 的 UID 会发生变更（Botim 4.0.2 客户端将使用 AUID 以支持 PayBy / Botim / Quantix 统一登录）
- 因此仍需要 bind-customer 接口：为老用户更新 UID、为新 4.0.2 用户创建 UID

## 兼容性要点（4.0 调研结论）

- 3.0 上的 Friend Transfer / Cash Gift / Household / Landing Page Reminder / Status Tracker 等通知，4.0 客户由 Botim 做兼容
- 以下 PayBy → Botim 的 callback / 查询接口由 Botim 兼容：
  - `/api/uaepay/payby/callback/getUserInfo`（Friend Transfer 收款方手机号查询/自动注册）
  - `/api/uaepay/payby/callback/isGiftMember`（Cash Gift 群成员校验）
  - `/api/buserrs/user/v1/inner/batchGetUidByMobile`
  - `/api/cuserrs/user/v1/userInfoDetail`
- 若 mobile 已存在系统中，无需校验即可更新对应 member 的 UID（与既有规则一致）
- 不允许客户回退到 Botim 3.0
- 手机号变更、注销重注册等场景见 [[botim-uid-mobile-change-cases]]

## Revision

| Date | Content | Author |
|---|---|---|
| 02 Apr 2025 | First edition | Zhibin |
| Jun 23, 2025 | 协议方案变更，复用 sgs http protocol；合并 authToken 与 login api | Huihua |
| 04 Sep 2025 | 调整 UID 兼容方案 | Huihua |
