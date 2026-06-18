---
id: tbl_reconciliation_balance_history
object_type: Table
domain: enbd-channel
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: wiki:f3f567ca-8ea1-4a6e-a466-ec15bae45776
tags:
- reconciliation
- balance
- history
subdomain: reconciliation
module: balance-monitor
sensitivity: normal
name: 渠道余额历史表
aliases: []
related_services: []
related_tables:
- tbl_reconciliation_balance_monitor
related_scenarios:
- enbd-balance-monitor-job
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
存储 `balanceMonitorJob` 触发余额查询后的余额变更历史记录。
- 由 reconciliation 余额监控定时任务落库。
- **余额没有变化时不会新增数据**（仅在余额发生变更时写入）。

## 关键列
原文未列出具体列结构，仅说明：
- 数据来源：cmf → router 查询渠道账户余额后回写。
- 与之配套的实时缓存：Redis key `_cmf:accountBalance:XXXXX`（XXXXX 为渠道账号）。

## 主键/索引
原文未提供。

## 校验点(QA 关注)
- 验证 `balanceMonitorJob` 触发后，仅在余额变化时才有新增记录，余额未变不应产生重复数据。
- 与 [[tbl_reconciliation_balance_monitor]] 中 `状态=Y` 的渠道账户配置联动：仅启用监控的账户应有历史数据。
- 与 Redis 缓存 `_cmf:accountBalance:XXXXX` 数据一致性核对。
- 排查"channel account balance is not enough"问题时，可通过本表与 Redis 缓存确认余额查询是否正常（参见 [[enbd-channel-troubleshooting]]）。
- 仅记录 scope 内：reconciliation.t_balance_history 余额变更历史，不涵盖出款交易明细。
