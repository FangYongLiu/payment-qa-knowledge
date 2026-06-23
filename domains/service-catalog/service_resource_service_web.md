---
id: svc_resource_service_web
object_type: Service
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp085
name: resource-service-web
dev_owner: 沈纲领
aliases: [gp085_resource-service-web]
related_services: []
related_tables: []
---

# resource-service-web

> APP 服务骨架。app_group=`gp085`,源=APP 清单。
> 当前归中性域 `service-catalog`(已激活、可检索)。上下游/API/表/业务细节待补。
> **认领可选**:某团队要为本服务建测试知识时,把 domain 改成 12 业务域之一 + 填
> owner + 补内容(见 docs/SERVICE_DOMAIN_CLAIM.md)。不认领则一直保持骨架。

## 同组服务（app_group=gp085，共 7 个模块）
- oauth-client-service-cgs-impl  (`svc_oauth_client_service_cgs_impl`)
- resource-service-cgs-impl  (`svc_resource_service_cgs_impl`)
- resource-service-rpc-dubbo-provider  (`svc_resource_service_rpc_dubbo_provider`)
- resource-service-sgs-impl  (`svc_resource_service_sgs_impl`)
- session-service-cgs-impl  (`svc_session_service_cgs_impl`)
- session-service-rpc-dubbo-provider  (`svc_session_service_rpc_dubbo_provider`)

## 待补（认领后）
- domain / owner：认领时填（默认 service-catalog / unassigned）
- 上下游 related_services：TODO（认领后按系统知识/架构图补）
- 涉及 API / 表：TODO
