---
title: Botim UID与手机号变更兼容场景
domain: channel-integration
kind: wiki_page
slug: botim-uid-mobile-change-cases
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:PMDPayment/1072791687
tags: []
---

# Botim UID与手机号变更兼容场景

本页聚焦 Botim 3.0 升级 4.0、4.0.2 引入 AUID、以及双方手机号/UID 变更与注销重注册等场景下，PayBy 与 Botim 的兼容策略和处理决策。

## 背景与影响点

- Botim 升级会导致 **Botim's UID would be changed**（UID 发生变化）。
- Botim 4.0.0 / 4.0.1：客户端 UID 与 Botim 3.0 兼容。
- Botim 4.0.2：客户端改为使用 **AUID**，统一 PayBy / Botim / Quantix 的登录身份；因此需要通过 [[api_personal_bind_customer]] 来：
  - 为老用户更新 UID；
  - 为新 4.0.2 用户创建 UID。

## 3.0 升级 4.0 的 UID 替换策略

通过 `/personal/v1/bind-customer` 按手机号绑定客户，并支持以 Old UID 替换 Member 的 UID。

按手机号绑定客户的处理矩阵：

| 场景 | 处理动作 |
|---|---|
| Same Mobile、UID existed | idempotent，返回已存在的 member |
| Mobile not exist PayBy member | Create member |
| Mobile exist PayBy member but no Botim UID associated | Bind with exist member |
| Mobile exist Botim UID 且与 Botim Old UID 相同（仅 3.0→4.0） | User's UID is same for botim3.0 / botim4.0，Replace Botim UID |
| Mobile exist Botim UID 且与 Botim Old UID 不同 | Not allow to do anything |

Replace UID 参数（M=必填）：
- Member ID - M
- Old Botim UID - M
- New Botim UID - M

详见 [[api_personal_bind_customer]]、[[botim-payby-server-integration-overview]]。

## Mobile / UID 变更与注销场景

需要兼容处理的场景清单：

- Botim 换手机
- PayBy 换手机
- PayBy 换手机 → 新手机已经存在 member，会被替换成 null 的流程
- Botim 注销后重新注册
- PayBy 注销后重新注册

关键决策：

- **Botim 侧手机号变更，PayBy 仍持有旧手机号**：保持原状（Keep it same as before），方案后续再讨论。
- **手机号已存在系统中，更新对应 member 的 UID 是否需要校验**：No need any verification，保持原状（来自 Yun 的确认）。
- **是否允许客户回退到 Botim 3.0**：Not allow（来自 Long 的决策）。

## 3.0 → 4.0 已知兼容问题

- sgs 网络互通问题，涉及到加解密（参见 [[botim-payby-payload-security]]）。
- 好友转账功能 3.0 升级到 4.0 无法领取。
- 升级到 4.0 后，数据层面出现前后不一致的情况。

## 仅 3.0 存在的通知/查询类 API 兼容

3.0 上才有的 Notification of Friend Transfer / Cash Gift / Household / Landing Page Reminder / Status Tracker 等，但用户已在 4.0 版本：**Botim will make it compatible**。

涉及 PayBy 调用 Botim 的接口（详见 [[botim-payby-outbound-apis]]）：

- 好友转账场景 —— 接收方未注册 PayBy 时通过 UID 查询手机号：
  - `/api/uaepay/payby/callback/getUserInfo` —— Botim 4.0 兼容。
- 红包/Cash Gift 场景：
  - `/api/uaepay/payby/callback/isGiftMember`（检查是否在官方红包群） —— Botim 4.0 兼容。
- 通过 Botim API 获取用户信息，Botim 3.0 是否兼容：Botim will make it compatible，包括：
  - `/api/buserrs/user/v1/inner/batchGetUidByMobile`
  - `/api/uaepay/payby/callback/getUserInfo`
  - `/api/cuserrs/user/v1/userInfoDetail`

## 4.0.2 是否仍需要 bind-customer

**Yes**。原因：

- 4.0.0 / 4.0.1 阶段 UID 与 3.0 兼容，理论上无需变更。
- 4.0.2 改用客户端 AUID 实现 PayBy / Botim / Quantix 统一登录，因此必须保留并使用 [[api_personal_bind_customer]]：
  - 老用户：更新 UID（Replace UID）；
  - 新 4.0.2 用户：创建 UID（Create / Bind UID to Member）。

## 相关页面

- [[botim-payby-server-integration-overview]]
- [[api_personal_bind_customer]]
- [[api_personal_login_or_refresh]]
- [[api_personal_v3_auth_login]]
- [[botim-payby-outbound-apis]]
