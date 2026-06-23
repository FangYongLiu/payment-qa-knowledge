---
id: ts_enbd_channel_balance_not_enough
object_type: Troubleshooting
domain: channel-integration
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: confluence:tester/1064206364
tags:
- ENBD
- 余额校验
- 出款
subdomain: null
module: null
sensitivity: normal
name: ENBD渠道余额不足报错排查
aliases: []
related_services: []
related_tables:
- reconciliation.t_balance_monitor
- reconciliation.t_balance_history
- router.t_channel_ext
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 症状
router 日志提示 ENBD 渠道 `channel account balance is not enough.`，导致出款被拦截。

## 可能根因
- 渠道账户余额确实不足（payoutAccount 实际余额低于阈值）。
- 余额监控 job（balanceMonitorJob）未及时刷新缓存数据，redis `_cmf:accountBalance:XXXXX` 中余额未更新。
- 对方银行系统波动，导致余额查询/出款瞬时异常。

## 排查步骤(DB/Kibana)
1. 确认渠道是否配置 payoutAccount（router 仅在 ext 配置 payoutAccount 时进行余额校验）：
   ```sql
   select * from router.t_channel_ext
   where channel_code in ('ENBD201','ENBD204','ENBD205')
   and attr_key = 'payoutAccount';
   ```
2. 通过 counter（balance monitor 规则）或 redis 缓存 `_cmf:accountBalance:XXXXX`（XXXXX 为渠道账号）确认余额查询是否正常。
3. 查看 reconciliation.t_balance_history 最新余额数据（余额没有变化不会新增数据）。
4. Kibana 检索关键字：`开始 余额监控 定时任务`，确认 balanceMonitorJob 是否正常触发并完成查询。
5. 核对 reconciliation.t_balance_monitor 表中对应渠道记录状态是否为 Y。

## 处理
- 若 counter 或 redis 显示余额正常：尝试再次发起出款，可能是对方系统瞬时波动。
- 若余额确实不足：联系运营进行渠道账户充值/调拨后再发起出款。
- 若余额查询 job 异常：排查 balanceMonitorJob 日志，确认 reconciliation → cmf → router 链路是否正常。
