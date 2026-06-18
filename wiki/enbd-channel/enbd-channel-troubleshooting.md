---
title: ENBD渠道常见问题排查
domain: enbd-channel
kind: wiki_page
slug: enbd-channel-troubleshooting
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:f3f567ca-8ea1-4a6e-a466-ec15bae45776
tags: []
---

# ENBD渠道常见问题排查

本页汇总 ENBD 渠道在余额校验、出款发起过程中常见的报错场景与排查思路。

## 余额不足报错

**现象**：router 日志提示 `ENBD 渠道 channel account balance is not enough.`

**排查步骤**：

1. 通过 counter 或 redis 缓存（key 形如 `_cmf:accountBalance:XXXXX`）确认当前余额查询是否正常。
2. 如余额数据正常，可尝试再次发起出款 —— 可能为对方系统瞬时波动导致。

**相关背景**：
- 余额数据来源参见 [[enbd-balance-monitor-job]]，落库表 [[tbl_reconciliation_balance_history]]，监控配置表 [[tbl_reconciliation_balance_monitor]]。
- 出款时 router 会判断渠道 ext 是否配置 `payoutAccount`，若配置则进行渠道余额校验，否则跳过；详见 [[enbd-fundout-flow]]。

## 排查切入点速查

- **确认查询账户**：在 `router.t_channel_ext` 中查 `attr_key='payoutAccount'` 对应的账户，确认监控查询的是真实出款账户。
- **确认 Job 是否运行**：搜索日志关键字 `开始` / `余额监控` / `定时任务`，定位 balanceMonitorJob 执行情况。
- **确认余额是否更新**：`reconciliation.t_balance_history` 在余额无变化时不会新增数据，需结合 redis 缓存判断最新值。
- **端到端排查**：参考 [[flow_enbd_fundout]] 与 [[enbd-channel-overview]]。
