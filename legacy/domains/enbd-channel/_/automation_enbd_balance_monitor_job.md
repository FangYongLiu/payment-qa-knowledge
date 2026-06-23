---
id: auto_enbd_balance_monitor_job
object_type: AutomationAsset
domain: channel-integration
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: confluence:tester/1064206364
tags:
- job
- balance
- monitor
subdomain: null
module: reconciliation
sensitivity: normal
name: ENBD余额监控定时任务
aliases:
- balanceMonitorJob
related_services: []
related_tables:
- reconciliation.t_balance_monitor
- reconciliation.t_balance_history
- router.t_channel_ext
related_scenarios: []
related_logs:
- 开始余额监控定时任务
related_requirements: []
related_failures:
- ts_enbd_channel_balance_not_enough
---

## 用途
定时查询 ENBD 渠道账户余额，并将结果落库与缓存，供出款时进行渠道余额校验使用。

## 使用方式
- 调用链路：reconciliation(balanceMonitorJob) → cmf → router
- 执行逻辑：
  1. reconciliation 获取 `reconciliation.t_balance_monitor` 表中 状态=Y 的数据
  2. 调用 cmf，参数包含：渠道号、账户类型、银行、阈值
  3. cmf 调用 router，router 根据 `channelCode`、`apiType=DB` 找到渠道，拿渠道对应账户去查询余额
- 余额查询规则配置入口：counter – account – balance monitor
- 日志关键字：`开始余额监控定时任务`

## 关键配置
- 规则配置表：`reconciliation.t_balance_monitor`（状态=Y 才会被 job 拉取）
- 渠道真实查询账户配置（router）：
  ```sql
  select * from router.t_channel_ext
  where channel_code in ('ENBD201','ENBD204','ENBD205')
    and attr_key = 'payoutAccount'
  ```
- 一期限制：规则与交易阈值共用数据，**一个账户只能配置一条规则**

## 注意事项
- 落库表：`reconciliation.t_balance_history`，**余额没有变化时不会新增数据**
- 落地 redis 缓存 key：`_cmf:accountBalance:XXXXX`（XXXXX 为渠道账号）
- 出款时 router 会判断渠道 ext 是否配置 `payoutAccount`，已配置才会进行渠道余额校验，否则跳过
- 当 router 报 `ENBD 渠道 channel account balance is not enough` 时，可通过 counter 或 redis 确认余额查询是否正常，详见 [[ts_enbd_channel_balance_not_enough]]
