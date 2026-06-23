---
id: svc_escrow
object_type: Service
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp104
name: escrow
dev_owner: 王迁
aliases: [gp104_escrow]
related_services: [svc_deposit, svc_voucher, svc_ues_ws, svc_ufs2]
related_tables: []
---

# escrow

> 来源:UAT Kibana trace 观测(2026-06-22~23 UAT cgs 回归窗口,真实但非穷尽)+ 作用说明。候选待人审。app_group=`gp104` · domain=`service-catalog`。

## 作用
担保 / 托管交易（推断：调 deposit/voucher/ues）  **(待核实:仅凭调用关系推断)**

## 系统中的位置
- 功能层:收单 / 收银 (Acquiring / Cashier)
- 业务域:`service-catalog`

## 关联关系
**调用(下游)—— 本服务依赖这些服务完成处理:**
- [[svc_deposit]] deposit（充值 / 存款服务） · 350 次 · high
- [[svc_voucher]] voucher（全局 ID 与幂等凭证） · 280 次 · high
- [[svc_ues_ws]] ues-ws（用户事件 / 数据服务） · 245 次 · med·待核实
- [[svc_ufs2]] ufs2（用户文件 / 数据服务） · 66 次 · med·待核实
