---
id: svc_mns_scheduler
object_type: Service
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp037
name: mns-scheduler
dev_owner: Yadong.Lu
aliases: [gp037_mns-scheduler]
related_services: [svc_ues_ws, svc_member]
related_tables: []
---

# mns-scheduler

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp037` · domain=`payment-core`。

## 作用
消息通知调度（定时通知，调 ues）

## 系统中的位置
- 功能层:通知 / 消息 (Notification)
- 业务域:`payment-core`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_ues_ws]] ues-ws（用户事件 / 数据服务） · 1688 次 · med·待核实
- [[svc_member]] member（会员 / 账户核心） · 6 次 · high

## 涉及的 API / 数据库表
- **暴露/相关 API**:待补
- **读写的表**:待补

## 关键方法 / 入口
- 待补(本窗口未单独抽取 Dubbo/RPC 方法级)。

## 测试要点 / 排障 / 常见问题

**UAT Kibana 7d 错误观测**(自动回归 + UAT 流量,app_id=`mns-scheduler`):
- ERROR 4 次(均为基础设施健康检查噪声,无显著业务错误)
- WARN 8929 次,主要:`NotifySendServiceImpl`×3
- ⚠️ 频次可能含 UAT 测试数据噪声,**真坑 vs 噪声需人工确认**;高频项见域级排障对象。
- 更多 QA 校验点(怎么测 / 已知坑 / 典型故障定位)待补。
## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp037` · domain=`payment-core`。
