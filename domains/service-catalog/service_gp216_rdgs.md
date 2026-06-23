---
id: svc_rdgs
object_type: Service
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp216
name: rdgs
dev_owner: 喻赛
aliases: [gp216_rdgs]
related_services: [svc_query, svc_ufs2]
related_tables: []
---

# rdgs

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp216` · domain=`service-catalog`。

## 作用
报表 / 数据服务（调 query/ufs）

## 系统中的位置
- 功能层:客服 / 内容 / 查询 / 其他 (CS / Content / Query / Misc)
- 业务域:`service-catalog`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_query]] query（查询 / 报表服务） · 2583 次 · high
- [[svc_ufs2]] ufs2（用户文件 / 数据服务） · 1097 次 · med·待核实
