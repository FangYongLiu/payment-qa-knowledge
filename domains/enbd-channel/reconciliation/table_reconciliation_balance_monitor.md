---
id: tbl_reconciliation_balance_monitor
object_type: Table
domain: enbd-channel
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: wiki:f3f567ca-8ea1-4a6e-a466-ec15bae45776
tags:
- balance
- monitor
- config
subdomain: reconciliation
module: balance-monitor
sensitivity: normal
name: 渠道余额监控配置表
aliases:
- reconciliation.t_balance_monitor
related_services: []
related_tables:
- tbl_reconciliation_balance_history
related_scenarios:
- enbd-balance-monitor-job
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
存储渠道余额监控规则配置数据。balanceMonitorJob 从本表获取状态=Y 的数据，调用 cmf 进行余额查询（参数：渠道号、账户类型、银行、阈值）。配置入口：counter – account – balance monitor。

一期因为规则和交易阈值共用数据，所以规则一个账户只能配置一条。

## 关键列
- 渠道号（channelCode）
- 账户类型
- 银行
- 阈值
- 状态（Y/N，仅 Y 参与 Job 调度）

## 主键/索引
原文未给出。

## 校验点(QA 关注)
- 状态=Y 的记录才会被 balanceMonitorJob 拉取并触发余额查询
- 同一账户只允许配置一条规则（一期限制，规则和交易阈值共用数据）
- 渠道是否真正参与余额查询，还需配合 router.t_channel_ext 中 attr_key='payoutAccount' 的配置（出款链路的余额校验依赖该 ext，与本表 Job 配置共同决定监控范围）
- 查询结果落库到 reconciliation.t_balance_history（余额没有变化不会新增数据），并写入 redis 缓存 `_cmf:accountBalance:XXXXX`
