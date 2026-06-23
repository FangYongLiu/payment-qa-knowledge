---
id: svc_cns
object_type: Service
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp289
name: cns
aliases: [gp289_cns]
related_services: [svc_member, svc_csimple]
related_tables: []
---

# cns

> 来源:UAT Kibana trace 观测(2026-06-22~23 UAT cgs 回归窗口,真实但非穷尽)+ 作用说明。候选待人审。app_group=`gp289` · domain=`service-catalog`。

## 作用
（推断：客户通知 / 客户服务，调 member/csimple）  **(待核实:仅凭调用关系推断)**

## 系统中的位置
- 功能层:客服 / 内容 / 查询 / 其他 (CS / Content / Query / Misc)
- 业务域:`service-catalog`

## 关联关系
**调用(下游)—— 本服务依赖这些服务完成处理:**
- [[svc_member]] member（会员 / 账户核心） · 866 次 · high
- [[svc_csimple]] csimple · 866 次 · high
