---
id: domain_infrastructure
object_type: Domain
name: infrastructure
aliases: [基础设施, 运维, 大数据, ops, bigdata]
domain: infrastructure
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-24'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: [infrastructure, 基础设施, 运维, 大数据, ops]
related_services: [svc_auth_server, svc_uae_data_server, svc_data_server, svc_mysql_member_sync, svc_feature_calculate_server_new, svc_crawl_leantech_server, svc_feature_calculate_server, svc_crawl_server, svc_dubbo_admin, svc_elasticjob_console, svc_spring_cloud_config, svc_spring_boot_admin, svc_data_etl, svc_cloud_mis, svc_bigdata_router, svc_sqlmonitor, svc_cicd, svc_cgs_apitest, svc_bigdata_router_admin, svc_at_beb, svc_resource_service_sgs_impl, svc_resource_service_rpc_dubbo_provider, svc_session_service_cgs_impl, svc_resource_service_web, svc_session_service_rpc_dubbo_provider, svc_oauth_client_service_cgs_impl, svc_resource_service_cgs_impl]
---

# infrastructure(基础设施 / 运维 / 大数据)

> 业务域总览。承载基础设施、运维平台、大数据相关服务。域 lead 待指定(owner=unassigned)。

## 概述
基础设施 / 运维 / 大数据域:平台基础组件(注册中心/配置中心/调度/监控)、运维平台(CICD/MIS)、
大数据(数据同步/抓取/特征计算/ETL/bigdata 路由)、QA 测试平台等非业务功能服务。

## 覆盖范围 / 负责人
- **大数据 / 数据平台(Yunfei.Ma)**:mysql-member-sync、data-server、uae-data-server、auth_server、crawl-server、crawl-leantech-server、feature-calculate-server(+new)
- **平台基础组件(Cong.Zhou)**:spring-boot-admin、spring-cloud-config、dubbo-admin、elasticjob-console
- **bigdata 路由(Kui.Luo)**:bigdata-router、bigdata-router-admin
- **DBA**:sqlmonitor
- **OPS**:cloud-mis、data-etl、cicd
- **QA**:cgs-apitest

## QA 关注点
- 待补。
