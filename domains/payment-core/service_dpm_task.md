---
id: svc_dpm_task
object_type: Service
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp004
name: dpm-task
dev_owner: 周聪
aliases: [gp004_dpm-task]
related_services: []
related_tables: []
---

# dpm-task

> APP 服务骨架。app_group=`gp004`,源=APP 清单。
> 当前归中性域 `service-catalog`(已激活、可检索)。上下游/API/表/业务细节待补。
> **认领可选**:某团队要为本服务建测试知识时,把 domain 改成 12 业务域之一 + 填
> owner + 补内容(见 docs/SERVICE_DOMAIN_CLAIM.md)。不认领则一直保持骨架。

## 同组服务（app_group=gp004，共 3 个模块）
- dpm-accounting  (`svc_dpm_accounting`)
- dpm-manager  (`svc_dpm_manager`)

## 待补（认领后）
- domain / owner：认领时填（默认 service-catalog / unassigned）
- 上下游 related_services：TODO（认领后按系统知识/架构图补）
- 涉及 API / 表：TODO
