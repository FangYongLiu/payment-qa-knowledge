---
title: ENBD渠道出款流程
domain: channel-integration
kind: wiki_page
slug: enbd-channel-fundout-flow
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:tester/1064206364
tags: []
---

# ENBD渠道出款流程

ENBD出款由 fundout 经 cmf 路由到 router，router 根据渠道配置决定是否进行余额校验，再与银行进行异步状态交互。

## 调用链路

- 调用关系：fundout → cmf → router
- router 根据渠道路由到具体账户
- router 判断渠道 ext 是否配置 `payoutAccount`：
  - 有配置：进行渠道余额校验（依赖 [[enbd-channel-balance-monitor]]）
  - 无配置：跳过余额校验

## 渠道与银行交互

ENBD渠道与银行的交互为异步模式：

1. ENBD渠道先发送 SP，银行返回 `httpResponseStatus=202`，表示已接收请求，订单处理中
2. Payby 主动调用查询接口，银行可能返回的状态：
   - `ACCEPTED`
   - `IN_PROGRESS` — Transaction is in progress at the bank
   - `PROCESSED_BY_BANK`
   - `COMPLETED`
3. 银行通过状态变更通知主动推送最终状态

## 必填字段：countryCode / cityCode

- countryCode、cityCode 由渠道侧获取
- ENBD 和 INNER 渠道无需传 cityCode
- 仅在他行 IBAN 场景下，渠道才会调用 member 查询 city name

## Remark 字段逻辑

按优先级处理 Remark：

- a. 默认使用 memo 字段（提现场景：`Fundout`）
- b. memo 为空时，使用 purposeCode：
  - `FIS`：提现
  - `MWO`：转账到卡
  - （目前暂无 memo 为空的场景）
- c. 命中 `useMerchantName` 配置的商户：memo 使用 `商户名称 + 地址`
- d. 命中 `merchantDynamic` 配置的商户：直接替换 memo 内容

## 渠道账户与场景对应

不同业务场景下走不同的 ENBD 渠道编码，并对应各自的待清算账户与银存账户，详见 [[enbd-channel-account-mapping]]。覆盖场景：

- 商户出款：ENBD201 / ENBD202 / ENBD203
- 个人出款：ENBD204 / ENBD205
- 资金调拨：ENBD209 / ENBD210

## 相关排查

- 出款报 `channel account balance is not enough`：见 [[ts_enbd_channel_balance_not_enough]]
- 渠道总体说明：见 [[enbd-channel-overview]]
- 常见问题汇总：见 [[enbd-channel-troubleshooting]]

## 参考资料

- Fund out PRD：https://algento.atlassian.net/wiki/x/P4DGJQ
- counter PRD：https://algento.atlassian.net/wiki/x/PgBfJg
- 个人提现 PRD：https://algento.atlassian.net/wiki/spaces/BOT/pages/732168261/ENBD
- 测试环境 IBAN：
  - EBILAED：`AE780260001015795438201`
  - MEBLAED：`AE800340003707336602101`
  - FGBMAEAA：`AE780271091001071667018`
