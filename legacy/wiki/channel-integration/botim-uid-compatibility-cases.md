---
title: Botim UID兼容与手机号变更案例
domain: channel-integration
kind: wiki_page
slug: botim-uid-compatibility-cases
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:a01637cc-4974-45c3-b1e9-d194dac7ed1f
tags: []
---

# Botim UID兼容与手机号变更案例

本页汇总 Botim 3.0 升级 4.0、4.0.2 引入 AUID 统一登录、以及手机号变更/注销重注册等场景下，Botim UID 与 PayBy member 关系的兼容处理规则与影响点。

## 背景与影响点
- Botim 升级会导致 Botim 的 UID 发生变化（Impacted Point: Botim's UID would be changed）。
- Botim 4.0.0 / 4.0.1：UID 与 Botim 3.0 兼容。
- Botim 4.0.2：客户端启用 AUID，用于支撑 PayBy / Botim / Quantix 的统一登录。
  - 因此需要 [[api_personal_bind_customer]] 来：
    - 为已有用户更新 UID；
    - 为新的 4.0.2 用户创建 UID。
- 不允许客户回退到 Botim 3.0（决策来自 Long）。

## Bind Customer 的场景判定
[[api_personal_bind_customer]] 按手机号 + UID + Old UID 的匹配关系决定行为：

| 场景 | 处理 |
|---|---|
| 同手机号、UID 已存在 | 幂等，返回已存在 member |
| 手机号在 PayBy 不存在 | 创建 member |
| 手机号已存在 PayBy member，但未关联 Botim UID | Bind with exist member |
| 手机号已存在 Botim UID，且与 Botim Old UID 相同（仅 3.0→4.0） | Replace Botim UID（用户的 UID 在 botim3.0/botim4.0 相同） |
| 手机号已存在 Botim UID，且与 Botim Old UID 不同 | 不允许任何操作 |

Replace UID 时 personal 侧支持通过 Old UID 替换 member 的 UID（参数：Member ID、Old Botim UID、New Botim UID）。

## 3.0 升级 4.0 的 UID 兼容
- 在 4.0.0 / 4.0.1，UID 与 3.0 兼容，3.0 时期对接的 Outbound API 由 Botim 侧做兼容（见下文清单）。
- 在 4.0.2，客户端切换为 AUID，此时通过 Bind Customer 完成：
  - Disassociate 3.0 Botim UID from member；
  - Associate 4.0 Botim UID with member；
  - Sign basic account protocol and TOU（如首次进入 4.0 钱包）。

## AUID 统一登录
- 4.0.2 客户端使用 AUID，实现 PayBy / Botim / Quantix 三端统一登录。
- 服务端登录入口合并为 [[api_personal_v3_auth_login]]（合并原 `/personal/apply/authToken` 与 `/personal/v2/auth/login`，向客户端返回 access token）。
- 服务端登录与刷新见 [[api_personal_login_or_refresh]]，详细网关协议见 [[botim-payby-server-integration-overview]] 与 [[botim-payby-grpc-gateway-protocol]]。

## 手机号变更与注销重注册
列入待处理/讨论的兼容案例：
- Botim 换手机
- PayBy 换手机
- PayBy 换手机 → 新手机已存在 member，会被替换成 null 的流程
- Botim 注销后重新注册
- PayBy 注销后重新注册

规则与决策：
- 若 Botim 侧手机号变更，但 PayBy 仍持有旧号：保持现状，方案后续讨论。
- 若手机号已存在系统中，可在无需校验的情况下更新对应 member 的 UID（来自 Yun 的决策）。

## 3.0 时期通知/查询 API 的兼容
客户已在 4.0 但通知（好友转账 / Cash Gift / Household / Landing Page Reminder / Status Tracker 等）仅在 3.0：
- Botim 侧负责兼容。

具体被点名兼容的 Outbound API（详见 [[botim-payby-outbound-apis]]）：
- 好友转账查询收款人手机号：`/api/uaepay/payby/callback/getUserInfo`
- Cash Gift 在群校验：`/api/uaepay/payby/callback/isGiftMember`
- 用户信息相关：
  - `/api/buserrs/user/v1/inner/batchGetUidByMobile`
  - `/api/uaepay/payby/callback/getUserInfo`
  - `/api/cuserrs/user/v1/userInfoDetail`

## 其他已知风险点
- sgs 网络互通问题，涉及到加解密（参见 [[botim-payby-payload-encryption]]）。
- 好友转账功能 3.0 升级到 4.0 无法领取。
- 升级到 4.0 后，数据层面出现前后不一致的情况。
