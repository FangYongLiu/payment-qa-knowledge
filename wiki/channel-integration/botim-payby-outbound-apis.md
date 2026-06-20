---
title: PayBy调用Botim Outbound API清单
domain: channel-integration
kind: wiki_page
slug: botim-payby-outbound-apis
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:a01637cc-4974-45c3-b1e9-d194dac7ed1f
tags: []
---

# PayBy调用Botim Outbound API清单

本页汇总 PayBy 侧调用 Botim 的 Outbound API 清单，覆盖用户信息查询、群组成员校验、通知推送、卡片消息、Widget 等场景。上层协议与加解密详见 [[botim-payby-grpc-gateway-protocol]] 与 [[botim-payby-payload-encryption]]，整体方案参见 [[botim-payby-server-integration-overview]]。

## 用户信息与 UID 查询

| API Code | Usage | Product / Cases | 调用方 |
|---|---|---|---|
| `/api/uaepay/payby/callback/getUserInfo` | Inquiry User Info by UID | Friend Transfer 等：member 创建（CreatePersonalMemberByUidProcessor）；socialpay AA split (`/socialpay/sb/sendSplitBill`、`/socialpay/sb/v1/auth/collection-money`)；basis-cms Query by UID；sgs Partner check (`/common/partner/checkWhitelist`)；personal Transfer to mobile init (`/personal/transfer/submit`)、Mobile different check (`/personal/mobile/different/check`)；接收方未注册 PayBy 时通过 Botim UID 查询手机号并自动注册 | member / socialpay / basis-cms / personal / sgs / remittance* |
| `/api/cuserrs/user/v1/userInfoDetail` | Inquiry User Info by Auth Code；配套 `/personal/auth/oauthByAuthCode`、`/personal/auth/loginByAuthCode`、`/personal/auth/followOA` | 基础接口 | personal / marketing-event* / member-future* / comp-service* |
| `/api/buserrs/user/v1/inner/batchGetUidByMobile` | Inquiry UID by Mobile Number | household（Receiver remind、Transfer fail notification、Transfer remind）、basis-cms（Query UID by mobile） | household / basis-cms |
| `/api/buserrs/user/v1/batchGetUserBaseInfo` | Batch Get User Info | — | marketing-event* / member-future* / comp-service* |

UID 兼容与手机号变更相关的具体 case 见 [[botim-uid-compatibility-cases]]。

## 群组与红包成员校验

| API Code | Usage | Product | 调用入口 |
|---|---|---|---|
| `/api/uaepay/payby/callback/isGroupMember` | Check in group or not | Cash Gift（Collect cash gift check） | `/socialpay/redpkg/receive`（socialpay） |
| `/api/uaepay/payby/callback/isGiftMember` | Check in official cash gift group or not | Official Cash Gift (Marketing) | `/socialpay/redpkg/receive`（socialpay） |

## OAuth 与公众号关注

| API Code | Usage |
|---|---|
| `/api/authserver/oauth2/token` | OAuth，基础接口（personal） |
| `/api/officialrs/subscribe/v1/follow` | Follow Official Account（marketing-event* / member-future* / comp-service*） |
| `/api/cstatistics/stats/v1/numberOfCallsToday` | Statistics Number of Calls Today（同上） |

## VIP 发放

| API Code | Usage | 场景 |
|---|---|---|
| `/api/buserrs/user/v1/giveOutVip` | Give Customer Botim VIP | Old Marketing（mssii*） |
| `/api/buserrs/user/v1/checkGiveOutVipStatus` | Check Give Status | Old Marketing（mssii*） |

## 卡片消息（Household 等）

| API Code | Usage | Product |
|---|---|---|
| `/api/officialrs/msg/v1/sendShoppingCartCardMsg` | Send Card | Household |
| `/api/officialrs/msg/v1/sendSubmitShoppingCartResponse` | Send Card Response | Household |
| `/api/officialrs/msg/v1/sendShoppingCartCardEvent` | Send Card Event | Household |
| `/api/payby/v1/inner/sendRichTextCard` | Send Card | Household |
| `/api/payby/v1/inner/sendRichTextCardUpdate` | Send Card | Household |

## Landing Page Todo

| API Code | Usage | 场景 |
|---|---|---|
| `/api/buserrs/lpage/upsertTodo` | Add or Update Todo Card | Landing Page：Low balance remind、Apply card remind、Exchange rate update remind 等（cns / remittance） |
| `/api/buserrs/lpage/closeTodo` | Close Todo Card | 同上 |

## Status Tracker / Widget

| API Code | Usage | Product |
|---|---|---|
| `/api/buserrs/explore/v1/upsertWidgetItem` | Add or Update Widget | Status Tracker（remittance） |
| `/api/buserrs/explore/v1/getWidgetItem` | Get Widget | Status Tracker（remittance） |
| `https://openapi.botim.me/api/buserrs/explore/v1/updateUserWidgetData` | Update User Widget Data | Mobile Top-Up |

## 通用通知推送

| API Code | Usage | 场景 |
|---|---|---|
| `https://uaepaygw.botim.me/api/uaepay/payby/callback/notify` | Send Specific Notification to User | Friend Transfer / Cash Gift / Aani Transfer（socialpay / personal / ons） |

## 4.0 兼容说明

- 4.0 用户场景下，3.0 时代的 Friend Transfer / Cash Gift / Household / Landing Page Reminder / Status Tracker 等通知，由 Botim 侧负责兼容。
- Friend Transfer 收款方未注册时通过 `/api/uaepay/payby/callback/getUserInfo` 查询手机号，由 Botim 兼容。
- Cash Gift 领取时通过 `/api/uaepay/payby/callback/isGiftMember`、`/api/uaepay/payby/callback/isGroupMember` 校验，由 Botim 兼容。
- 用户信息类接口（`batchGetUidByMobile`、`getUserInfo`、`userInfoDetail`）由 Botim 3.0 侧兼容。
- 标注 `*` 的系统名（如 remittance*、marketing-event*、member-future*、comp-service*、mssii*）为原文未定稿/待确认的调用方系统。

> PayBy 侧入站接口（`/personal/v1/bind-customer`、`/personal/v1/login-or-refresh`、`/personal/v3/auth/login`）见 [[api_personal_bind_customer]]、[[api_personal_login_or_refresh]]、[[api_personal_v3_auth_login]]。
