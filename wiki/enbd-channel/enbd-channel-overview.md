---
title: ENBD渠道总览
domain: enbd-channel
kind: wiki_page
slug: enbd-channel-overview
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:tester/1064206364
tags: []
---

# ENBD渠道总览

本页汇总 ENBD 渠道相关的 PRD 入口、测试 IBAN、出款流程要点与账户配置，作为 ENBD 渠道知识的导航页。

## PRD 文档入口

- Fund out PRD: https://algento.atlassian.net/wiki/x/P4DGJQ
- Counter PRD: https://algento.atlassian.net/wiki/x/PgBfJg
- 个人提现部分 PRD: https://algento.atlassian.net/wiki/spaces/BOT/pages/732168261/ENBD

## 测试环境测试 IBAN

- EBILAED：`AE780260001015795438201`
- MEBLAED：`AE800340003707336602101`
- FGBMAEAA：`AE780271091001071667018`

## 渠道余额查询机制（概述）

通过 `balanceMonitorJob` 定时任务读取 `reconciliation.t_balance_monitor` 中状态=Y 的规则，经 cmf → router 路由到对应渠道账户查询余额，结果落库 `reconciliation.t_balance_history` 并写入 Redis 缓存 `_cmf:accountBalance:XXXXX`。

详细逻辑、配置 SQL、日志关键字见 [[enbd-channel-balance-monitor]] / [[auto_enbd_balance_monitor_job]]。

## 出款流程（概述）

fundout → cmf → router，router 路由渠道时若渠道 ext 配置了 `payoutAccount` 则进行渠道余额校验，否则跳过；之后渠道与银行交互（SP 提交、查询、状态通知）。

字段获取（countryCode / cityCode）、Remark 字段拼装规则、与银行交互的状态流转详见 [[enbd-channel-fundout-flow]] / [[flow_enbd_fundout]]。

## 渠道账户配置（概述）

ENBD 渠道按业务场景（商户出款 / 个人出款 / 资金调拨）和卡类型（INNER / DFT / IFT）拆分多个 channelCode（ENBD201–ENBD210），每个 channelCode 对应不同的待清算账户与银存账户。

完整映射表见 [[enbd-channel-account-mapping]]。

## 常见问题

- router 日志报 `channel account balance is not enough`：先确认 counter 或 Redis 中余额是否正常，正常则可重试出款，可能为对方系统瞬时波动。

完整排查思路见 [[enbd-channel-troubleshooting]] / [[ts_enbd_channel_balance_not_enough]]。
