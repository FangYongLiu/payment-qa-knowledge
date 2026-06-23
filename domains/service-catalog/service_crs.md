---
id: svc_crs
object_type: Service
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp258
name: crs
aliases: [gp258_crs]
related_services: [svc_member, svc_voucher]
related_tables: []
---

# crs

> 来源:UAT Kibana trace 观测(2026-06-22~23 UAT cgs 回归窗口,真实但非穷尽)+ 作用说明。候选待人审。app_group=`gp258` · domain=`service-catalog`。

## 作用
（推断：客户 / 风控相关，调 member/voucher）  **(待核实:仅凭调用关系推断)**

## 系统中的位置
- 功能层:客服 / 内容 / 查询 / 其他 (CS / Content / Query / Misc)
- 业务域:`service-catalog`

## 关联关系
**调用(下游)—— 本服务依赖这些服务完成处理:**
- [[svc_member]] member（会员 / 账户核心） · 24 次 · high
- [[svc_voucher]] voucher（全局 ID 与幂等凭证） · 24 次 · high
