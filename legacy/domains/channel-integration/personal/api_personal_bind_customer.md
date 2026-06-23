---
id: api_personal_bind_customer
object_type: API
domain: channel-integration
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: confluence:PMDPayment/1072791687
tags:
- bind
- member
- UID
- mobile
subdomain: personal
module: sgs-api
sensitivity: normal
name: 绑定客户接口 (bind-customer)
aliases:
- Bind Customer
- /personal/v1/bind-customer
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
- 用于 Botim 4.0 客户首次使用钱包功能时，根据手机号与 Botim UID 在 PayBy 创建/绑定/替换 member 的接口。
- 支持的场景：
  - Create member：手机号在 PayBy 不存在 member 时，新建 member，并激活 AED BASIC 账户、签署 basic account 协议与 TOU。
  - Bind with exist member：手机号已存在 PayBy member 但未绑定 Botim UID，将 4.0 Botim UID 与 member 关联，并签署协议与 TOU。
  - Replace Botim UID（3.0 升级 4.0）：手机号已绑定 Botim UID，且与 Old Botim UID 一致时，解绑 3.0 UID 并绑定 4.0 UID。
- 在 Botim 4.0.2 中仍需此接口：客户端使用 AUID 支持 Payby/Botim/Quantix 统一登录，需通过该接口为老用户更新 UID、为新 4.0.2 用户创建 UID。

## 路径/方法
- API Code: `/personal/v1/bind-customer`
- 协议：通过 gRPC 网关调用（`at_df.DownstreamCaller.call`），ApplicationMessage.Meta.adm = `/personal/v1/bind-customer`。
- 文档地址：http://sim.intra.test2pay.com/api-doc/sgs-api/personal-sgs-api/

## 入参
请求 ApplicationMessage：
- Meta.adm：`/personal/v1/bind-customer`
- Meta.adh（Header）：
  - `partner-id`：Partner ID（如 `20000000006`）
  - `Content-Language`：`en` / `ar` / `zh`
- amp（JSON Payload，AES-256/GCM/NoPadding 加密，IV 16 字符前置，Base64 编码）

业务参数（M=必填，O=可选）：
- Mobile Number - M
- Botim UID（用于与 Botim 建立关系） - M
- Client IP - M
- Botim Old UID（可能为 3.0 UID） - O

## 出参
- Member ID - M（必返）

按手机号绑定的处理矩阵：

| 场景 | Action |
|---|---|
| 同手机号、UID 已存在 | 幂等，返回已存在的 member |
| 手机号在 PayBy 不存在 member | Create member |
| 手机号存在 PayBy member 但未绑定 Botim UID | Bind with exist member |
| 手机号已绑定 Botim UID 且与 Botim Old UID 相同（仅限 3.0→4.0） | Replace Botim UID |
| 手机号已绑定 Botim UID 且与 Botim Old UID 不同 | Not allow to do anything |

member 侧能力：
- Bind UID to Member：参数 Member ID(M) + Botim UID(M)
- Replace UID：参数 Member ID(M) + Old Botim UID(M) + New Botim UID(M)
- 备注：手机号已存在 system 时，更新对应 member 的 UID 无需任何额外验证（与原流程一致）。

## 错误码
- 原文未提供该接口的具体错误码清单。
- 仅给出语义约束：当手机号已绑定的 Botim UID 与传入的 Botim Old UID 不一致时，"Not allow to do anything"（不允许执行任何动作）。

## 测试校验点
- 幂等性：相同 Mobile + 相同 UID 重复调用，返回同一 Member ID，不产生新 member。
- 新建 member：手机号未在 PayBy 注册时，自动创建 member、激活 AED BASIC 账户、完成 basic account 协议与 TOU 签署。
- 已存在 member 未绑 UID：成功 Bind，并完成协议与 TOU 签署，返回 Member ID。
- 3.0 升级 4.0（UID 替换）：手机号当前绑定的 UID == Old Botim UID 时，解绑旧 UID，绑定新 UID。
- 拒绝替换：手机号当前绑定的 UID ≠ Old Botim UID 时，接口不应执行 create/bind/replace 任一动作。
- 必填校验：Mobile Number、Botim UID、Client IP 缺失时应失败；Botim Old UID 仅在 replace 场景使用，可选。
- Header 校验：`partner-id`、`Content-Language`(en/ar/zh) 正常透传。
- 报文安全：amp 使用 AES-256/GCM/NoPadding 加密，IV(16 字符) 前置 + Base64；解密侧能正确还原 JSON。
- Botim 4.0.2 兼容：使用 AUID 作为 UID 时，老用户 UID 更新与新用户 UID 创建均能通过本接口完成。
- 下游影响：成功后续可调用 `/personal/v1/login-or-refresh` 或 `/personal/v3/auth/login` 完成登录链路。
