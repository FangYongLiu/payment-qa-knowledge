---
title: ENBD渠道余额查询Job
domain: enbd-channel
kind: wiki_page
slug: enbd-balance-monitor-job
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:f3f567ca-8ea1-4a6e-a466-ec15bae45776
tags: []
---

# ENBD渠道余额查询Job

ENBD 渠道通过 `balanceMonitorJob` 定时拉取银行账户余额，落库历史并写入 Redis 缓存，供出款时的余额校验使用。相关上下文见 [[enbd-channel-overview]]、[[enbd-fundout-flow]]。

## 执行逻辑

- reconciliation 读取 [[tbl_reconciliation_balance_monitor]] 中 `状态=Y` 的数据
- 调用 cmf，传参：渠道号、账户类型、银行、阈值
- cmf 调用 router；router 根据 `channelCode` + `apiType=DB` 找到渠道，并拿渠道对应账户去查询余额
- 触发查询时日志关键字：`开始` / `余额监控` / `定时任务`

## 配置入口

- 通过 **counter – account – balance monitor** 配置余额查询规则
- 一期限制：规则与交易阈值共用数据，**一个账户只能配置一条规则**
- 渠道真实查询账户配置在 `router.t_channel_ext`：

```sql
select * from router.t_channel_ext
where channel_code in ('ENBD201','ENBD204','ENBD205')
  and attr_key = 'payoutAccount';
```

## 落库与缓存

- 余额历史落库到 [[tbl_reconciliation_balance_history]]
  - **余额无变化时不新增数据**
- 同时写入 Redis 缓存：
  - key 格式：`_cmf:accountBalance:XXXXX`（XXXXX 为渠道账号）

## 与出款的关系

- 出款链路 fundout → cmf → router 时，router 判断渠道 ext 是否配置 `payoutAccount`
  - 已配置：进行渠道余额校验（依赖本 Job 维护的余额数据）
  - 未配置：跳过校验
- 出款字段与流程详见 [[enbd-fundout-flow]]

## 常见问题

- router 日志提示 `ENBD 渠道 channel account balance is not enough`：
  - 通过 counter 或 Redis 确认余额查询是否正常
  - 若余额正常，尝试再次发起出款（可能对方系统波动）
  - 更多排查见 [[enbd-channel-troubleshooting]]
