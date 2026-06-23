---
title: ENBD渠道余额查询机制
domain: channel-integration
kind: wiki_page
slug: enbd-channel-balance-monitor
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:tester/1064206364
tags: []
---

# ENBD渠道余额查询机制

ENBD 渠道通过定时任务 `balanceMonitorJob` 周期性查询渠道账户余额，结果落库并写入 Redis 缓存，供出款时进行余额校验使用。相关出款逻辑见 [[enbd-channel-fundout-flow]]，账户与渠道映射见 [[enbd-channel-account-mapping]]。

## 任务执行链路

- 任务名：`balanceMonitorJob`（详见 [[auto_enbd_balance_monitor_job]]）
- 执行步骤：
  1. `reconciliation` 读取 `reconciliation.t_balance_monitor` 表中 `状态=Y` 的数据
  2. 调用 `cmf`，参数包含：渠道号、账户类型、银行、阈值
  3. `cmf` 调用 `router`，由 router 根据 `channelCode` + `apiType=DB` 找到渠道
  4. 拿渠道对应账户去查询余额
- 日志关键字：`开始`、`余额监控`、`定时任务`

## 配置方式

- 通过 `counter – account – balance monitor` 进行余额查询规则配置
- ⚠️ 一期因规则和交易阈值共用数据，**一个账户只能配置一条规则**
- 渠道真实查询账户配置查询 SQL：

```sql
select * from router.t_channel_ext
where channel_code in ('ENBD201','ENBD204','ENBD205')
  and attr_key = 'payoutAccount';
```

> 渠道是否参与余额校验，取决于其 `t_channel_ext` 是否配置了 `payoutAccount`；未配置则出款时跳过余额校验。

## 落库与缓存

- **监控规则表**：`reconciliation.t_balance_monitor`（任务读取数据源）
- **余额历史表**：`reconciliation.t_balance_history`
  - 注意：**余额没有变化时不会新增数据**
- **Redis 缓存** key：`_cmf:accountBalance:XXXXX`（XXXXX 为渠道账号）

## 与出款的关联

出款链路 `fundout → cmf → router` 中，router 会根据渠道 ext 的 `payoutAccount` 配置决定是否校验余额；当余额不足时报错 `channel account balance is not enough`，排查方法见 [[ts_enbd_channel_balance_not_enough]]。
