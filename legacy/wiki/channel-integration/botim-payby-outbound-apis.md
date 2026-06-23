---
title: PayBy调用Botim Outbound API清单
domain: channel-integration
kind: wiki_page
slug: botim-payby-outbound-apis
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:PMDPayment/1072791687
tags: []
---

# PayBy调用Botim Outbound API清单

本页汇总 PayBy 侧需要调用 Botim 的对外 API（Outbound APIs），按业务场景与所属系统归类，便于在好友转账、Cash Gift、Household、Landing Page、Status Tracker 等场景下定位接口与提醒触达通道。

> 协议层、加解密与登录绑定相关请见 [[botim-payby-server-integration-overview]]、[[botim-payby-grpc-gateway-protocol]]、[[botim-payby-payload-security]]。UID/手机号变更兼容场景见 [[botim-uid-mobile-change-cases]]。

## 用户信息与 UID 查询

用于按 UID/手机号反查用户信息，覆盖好友转账、AA Split、CMS 查询、自动注册等场景。

| API Code | 用途 | 场景 / 调用方系统 |
|---|---|---|
| `/api/uaepay/payby/callback/getUserInfo` | 通过 UID 查询用户信息 | Friend Transfer 等；调用方：member（`CreatePersonalMemberByUidProcessor` 按 UID 创建 member）、socialpay（AA Split：`/socialpay/sb/sendSplitBill`、`/socialpay/sb/v1/auth/collection-money`）、basis-cms（按 UID 查询）、sgs（`/common/partner/checkWhitelist` 合作方校验）、personal（好友转账初始化 `/personal/transfer/submit`、`/personal/mobile/different/check`），收款方未注册 PayBy 时通过 Botim UID 反查手机号并自动注册 |
| `/api/cuserrs/user/v1/userInfoDetail` | 通过 Auth Code 查询用户信息 | personal |
| `/api/buserrs/user/v1/batchGetUserBaseInfo` | 批量获取用户基础信息 | marketing-event*、member-future*、comp-service* |
| `/api/buserrs/user/v1/inner/batchGetUidByMobile` | 通过手机号反查 UID | household（收款人提醒、转账失败通知、转账提醒）、basis-cms（按手机号查 UID） |

## 群组与红包成员校验（Cash Gift）

用于领取红包/现金礼时校验用户是否在指定群或官方群。

| API Code | 用途 | 场景 |
|---|---|---|
| `/api/uaepay/payby/callback/isGroupMember` | 校验是否在群中 | Cash Gift 领取校验 `/socialpay/redpkg/receive`（socialpay） |
| `/api/uaepay/payby/callback/isGiftMember` | 校验是否在官方 Cash Gift 群中 | Official Cash Gift（Marketing）领取校验 `/socialpay/redpkg/receive`（socialpay） |

## OAuth 与登录授权

PayBy 端用于 OAuth 授权、按 Auth Code 登录、关注公众号等基础能力。

| API Code | 用途 | 调用方系统 |
|---|---|---|
| `/api/authserver/oauth2/token` | OAuth Token，基础 API | personal |
| `/personal/auth/oauthByAuthCode` | 通过 Auth Code 进行 OAuth | marketing-event*、member-future*、comp-service*、personal |
| `/personal/auth/loginByAuthCode` | 通过 Auth Code 登录 | personal |
| `/personal/auth/followOA` | 关注 Official Account | marketing-event*、member-future*、comp-service* |
| `/api/officialrs/subscribe/v1/follow` | 关注 Official Account | marketing-event*、member-future*、comp-service* |
| `/api/cstatistics/stats/v1/numberOfCallsToday` | 今日调用次数统计 | marketing-event*、member-future*、comp-service* |

> 注：PayBy 侧服务端登录入口对应 [[api_personal_v3_auth_login]]、[[api_personal_login_or_refresh]]，绑定客户见 [[api_personal_bind_customer]]。

## VIP 发放（Old Marketing）

| API Code | 用途 | 调用方系统 |
|---|---|---|
| `/api/buserrs/user/v1/giveOutVip` | 发放 Botim VIP | Old Marketing、mssii* |
| `/api/buserrs/user/v1/checkGiveOutVipStatus` | 校验 VIP 发放状态 | Old Marketing、mssii* |

## Household 卡片消息

Household 业务向用户发送购物车卡片、卡片更新与卡片事件，调用方均为 household。

| API Code | 用途 |
|---|---|
| `/api/officialrs/msg/v1/sendShoppingCartCardMsg` | 发送购物车卡片消息 |
| `/api/officialrs/msg/v1/sendSubmitShoppingCartResponse` | 发送提交购物车响应 |
| `/api/officialrs/msg/v1/sendShoppingCartCardEvent` | 发送购物车卡片事件 |
| `/api/payby/v1/inner/sendRichTextCard` | 发送富文本卡片 |
| `/api/payby/v1/inner/sendRichTextCardUpdate` | 更新富文本卡片 |

## Landing Page Todo 卡片

用于 Landing Page 提醒（低余额提醒、申请卡片提醒、汇率更新提醒等）。

| API Code | 用途 | 调用方系统 |
|---|---|---|
| `/api/buserrs/lpage/upsertTodo` | 新增/更新 Todo 卡片 | cns、remittance |
| `/api/buserrs/lpage/closeTodo` | 关闭 Todo 卡片 | cns、remittance |

## Status Tracker / Widget

用于 Status Tracker 与 Mobile Top-Up 等场景下的 Widget 维护与数据更新。

| API Code | 用途 | 调用方系统 |
|---|---|---|
| `/api/buserrs/explore/v1/upsertWidgetItem` | 新增/更新 Widget | remittance |
| `/api/buserrs/explore/v1/getWidgetItem` | 获取 Widget | remittance |
| `https://openapi.botim.me/api/buserrs/explore/v1/updateUserWidgetData` | 更新用户 Widget 数据 | Mobile Top-Up |

## 通用通知触达

| API Code | 用途 | 场景 / 调用方系统 |
|---|---|---|
| `https://uaepaygw.botim.me/api/uaepay/payby/callback/notify` | 向用户发送特定通知 | Friend Transfer / Cash Gift / Aani Transfer；socialpay、personal、ons |

## 4.0 兼容说明

- Friend Transfer / Cash Gift / Household / Landing Page Reminder / Status Tracker 等通知仅在 Botim 3.0，但用户可能升级到 4.0：Botim 侧负责兼容。
- 收款方未注册 PayBy 时，PayBy 通过 `/api/uaepay/payby/callback/getUserInfo` 反查手机号：Botim 侧兼容。
- Cash Gift 领取时的群成员校验 `/api/uaepay/payby/callback/isGiftMember`：Bot
