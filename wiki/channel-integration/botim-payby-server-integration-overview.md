---
title: Botim-PayBy Server端集成方案总览
domain: channel-integration
kind: wiki_page
slug: botim-payby-server-integration-overview
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:a01637cc-4974-45c3-b1e9-d194dac7ed1f
tags: []
---

# Botim-PayBy Server端集成方案总览

本页概述 Botim 4.0 与 PayBy 通过 gRPC 网关进行服务端集成的整体方案，覆盖绑定客户与登录两大业务范式，以及网关协议、加解密与对外 API 入口。

## 目标

- 实现 gRPC 网关
- 实现客户信息交换（绑定客户）
- 实现服务端登录与刷新 Token
- 兼容此前 PayBy 调用 Botim 的 API（详见 [[botim-payby-outbound-apis]]）

## 业务范式

### 3.1 Bind Customer（绑定客户）

触发与场景：
- **触发时机**：客户使用 Wallet 相关功能时
- **协议页展示**：客户首次使用 4.0 Wallet 时

`personal` 系统在 `4.1.1 Bind customer` 中负责创建/绑定/替换 Member，对应行为：
- **Create new member**：激活 AED BASIC 账户，签署 basic account protocol 与 TOU
- **Bind with exist member**：将 4.0 Botim UID 关联到既有 member，签署协议与 TOU
- **Replace Botim UID**（3.0 升级到 4.0）：解除 3.0 Botim UID 关联，关联 4.0 Botim UID

按手机号绑定的处理矩阵：

| 场景 | 动作 |
|---|---|
| Same Mobile、UID existed | 幂等，返回已存在的 member |
| Mobile not exist PayBy member | Create member |
| Mobile exist PayBy member but no Botim UID associated | Bind with exist member |
| Mobile exist Botim UID 且与 Botim Old UID 相同（仅 3.0→4.0） | Replace Botim UID |
| Mobile exist Botim UID 且与 Botim Old UID 不同 | 不允许任何操作 |

入参（M=Mandatory, O=Optional）：
- Mobile Number - M
- Botim UID - M
- Client IP - M
- Botim Old UID - O

返回：
- Member ID - M

`member` 系统支持的两类 UID 操作：
- **Replace UID**：Member ID(M)、Old Botim UID(M)、New Botim UID(M)
- **Bind UID to Member**：Member ID(M)、Botim UID(M)

绑定完成后，由 `personal` 通过服务端方式登录 PayBy（`4.3.1 Login`），入参 Member ID(M)、Botim UID(M)，返回 Access Token(M)。

接口详见 [[api_personal_bind_customer]] 与 [[api_personal_login_or_refresh]]。
关于 UID 兼容（4.0.0/4.0.1 与 4.0.2 AUID 切换）以及手机号变更的处理，参见 [[botim-uid-compatibility-cases]]。

### 3.2 Login for Customer（客户登录）

- 步骤 `1.2.1`：在 `personal` 新增 API `/personal/v3/auth/login`
- 该接口**合并** `/personal/apply/authToken` 与 `/personal/v2/auth/login`，向客户端直接返回 access token
- 接口详情见 [[api_personal_v3_auth_login]]
- 参考：Personal - Member Onboarding

## 网关定义

### gRPC 协议

- proto package：`at_df`
- service：`DownstreamCaller`，提供 `send(DFRequest) returns Empty` 与 `call(DFRequest) returns DFResponse`
- `DFResponse.status` 枚举：`OK = 0`、`ERROR = 1`
- 请求/响应消息体均为 `bytes message`

报文结构与字段详见 [[botim-payby-grpc-gateway-protocol]]，要点：
- `ApplicationMessage` 含 `version`、`id`(16 字节请求 ID)、`meta`、`amp`
- `Meta` 字段：`adn`/`adm`/`asn`/`asm`/`amt`/`amf`/`amh`/`ame`/`amc`(默认 `ComMode.CALL`)
- `adm`：标识被调 API，例如 `/personal/v1/bind-customer`
- `adh`（Header）示例：`partner-id`(如 `20000000006`)、`Content-Language`(`en,ar,zh`)
- `amp`：JSON 负载，结构示例
  ```json
  {
    "requestTime": 17691238142134,
    "bizContent": { "mobileNumber": "xxxx", "uid": "xxx" }
  }
  ```

### 请求安全（加解密）

完整规范与示例代码见 [[botim-payby-payload-encryption]]，要点：
- 算法：`AES/GCM/NoPadding`
- 密钥长度：AES-256
- IV 长度：16 字符（IV 拼接在密文之前）
- 加密结果使用 Base64 编码
- 实现常量：`GCM_TAG_LENGTH = 16`、`GCM_NONCE_LENGTH = 12`

## API 文档

Personal Documentation：`http://sim.intra.test2pay.com/api-doc/sgs-api/personal-sgs-api/`

| API Code | API Name |
|---|---|
| `/personal/v1/bind-customer` | Bind Customer |
| `/personal/v1/login-or-refresh` | Login or Refresh Token |
| `/personal/v3/auth/login` | Customer Login |

## 影响点

- Botim 的 UID 会发生变化（4.0.2 起客户端使用 AUID 实现 Payby/Botim/Quantix 统一登录），相关兼容详情见 [[botim-uid-compatibility-cases]]

## 4.0 兼容问答要点

- **3.0 专属通知**（Friend Transfer / Cash Gift / Household / Landing Page Reminder / Status Tracker 等）在 4.0 客户上的处理：Botim 兼容
- **Friend Transfer**：未注册 PayBy 时通过 `/api/uaepay/payby/callback/getUserInfo` 查询接收方手机号，Botim 兼容
- **Cash Gift**：通过 `/api/uaepay/payby/callback/isGiftMember` 校验是否在群内，Botim 兼容
- **用户信息查询接口**（Botim 3.0 兼容）：
  - `/api/buserrs/user/v1/inner/batchGetUidByMobile`
  - `/api/uaepay/payby/callback/getUserInfo`
  - `/api/cuserrs/user/v1/userInfoDetail`
- **Botim 手机号变更而 PayBy 仍持旧号**：保持现状，方案后续讨论
- **手机号已存在时更新对应 member 的 UID**：无需任何验证，与现状一致
- **是否允许客户回退到 Botim 3.0**：不允许
- **Botim 4.0.2 是否仍需 bind customer API**：需要。4.0.0/4.0.1 的 UID 与 3.0 兼容，4.0.2 客户端改用 AUID 实现统一登录，因此需通过 Bind Customer 为老用户更新 UID、为新 4.0.2 用户创建 UID

其他已知问题：
- sgs 网络互通涉及加解密
- 好友转账 3.0→4.0 升级后无法领取
- 升级
