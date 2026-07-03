---
id: svc_host
object_type: Service
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp150
name: host
dev_owner: Yadong.Lu
aliases: [gp150_host]
related_services: []
related_tables: []
---

# host

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp150` · domain=`payment-core`。

## 作用
**主机记账 / 交易事件监听**服务(gp150,UAT 近7d ~4.3 万条)。监听交易(支付)事件做主机侧记账,以发号器 + 补偿事件重试保证最终一致。

## 系统中的位置
- 功能层:账务 / 交易事件消费(Accounting / Event Consumer)
- 业务域:`payment-core`
- 驱动方式:MQ 事件监听 + 定时补偿(异步消费,非同步 RPC 入口)。

## 关联关系
**事件驱动**:`TradeListener` 监听 [[svc_tradeii]] 的支付/交易事件 → 主机记账;确认支付后的 MQ 扇出订阅方之一(见 [[flow_cashier_payment]] 异步长尾)。补偿事件由本地 job 重试。

## 关键方法 / 入口(UAT 实测 mClass)
- `TradeListener` —— 监听交易事件(主机记账)。
- `SegmentIDGenImpl` —— 发号器。
- `CompensationEventJob` / `CompensationEventRetryServiceImpl` —— 补偿事件与重试(最终一致)。

## 测试要点 / 排障 / 常见问题
- **异步记账**:确认支付后 host 通过 MQ 消费交易事件记账,属结算长尾(分钟→小时级),非同步链;定位时按交易凭证在 host 日志查 TradeListener 消费。
- **补偿一致性**:异常后补偿事件是否触发、重试幂等、最终账务一致。

## 相关流程 / 场景 / 排障(反向)
本服务涉及的流程/场景/排障(由对方 `related_services` 指向,反向汇总):
- [[flow_cashier_payment]](流程:收银台 / 收单卡支付端到端流程（含退款）)

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp150` · domain=`payment-core`。
