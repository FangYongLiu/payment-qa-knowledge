---
id: svc_deduct
object_type: Service
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp205
name: deduct
dev_owner: 刘智斌
aliases: [gp205_deduct]
related_services: [svc_protocol, svc_tradeii]
related_tables: []
---

# deduct

> 来源:UAT Kibana trace 观测(2026-06-22~23 UAT cgs 回归窗口,真实但非穷尽)+ 作用说明。候选待人审。app_group=`gp205` · domain=`service-catalog`。

## 作用
自动代扣执行（queryProtocol，调 protocol/trade）

## 系统中的位置
- 功能层:会员 / 账户 / 卡 / 协议 (Member / Account / Card)
- 业务域:`service-catalog`

## 关联关系
**调用(下游)—— 本服务依赖这些服务完成处理:**
- [[svc_protocol]] protocol（代扣 / 签约协议管理） · 32 次 · high
- [[svc_tradeii]] tradeii（交易订单引擎） · 15 次 · high

**被调用(上游)—— 这些服务调用本服务:**
tradeii

## 参与的业务场景(cgs 回归)
- §3. 自动代扣 / 签约（`test_auto_debit`）

## 观测到的对外方法
queryProtocol
