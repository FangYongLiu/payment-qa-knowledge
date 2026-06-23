---
title: PROD生产环境访问指南(基础设施/业务后台/门户)
domain: payby-core-systems
kind: wiki_page
slug: prod-env-access-guide
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:900cf819-4baf-4e3a-8c8b-28ae36b6df33
tags: []
---

# PROD生产环境访问指南(基础设施/业务后台/门户)

本页汇总 PROD 环境下基础设施、业务 Portal、其他门户的访问入口、账号说明及 Grafana 端口与 Redis 域名的映射关系，便于团队成员快速定位生产资源。

> 注：本页已 Migrated to: ENV-PROD；通用环境信息见「0-入职指南」。

## 基础设施 (Infrastructure)

| App Name | Description | URL | 备注 |
|---|---|---|---|
| Alhambra / appcenter | k8s portal | https://appcenter.corp.payby.com/ | — |
| skywalking | APM | https://skw.corp.payby.com/ | — |
| Log Kibana | es7 日志数据 | https://kibana.corp.payby.com/ | 索引：`java-logstash-*` (ANALYSIS)、`porter_cgs*` (ANALYSIS)、`porter_sgs*` (ANALYSIS)；Azure: `reader / reader_Qwer`；cgs,sgs user: `porter_user`；app_log user: `app_log_user` |
| Business Kibana | es7 业务数据 | https://esdata-kibana.corp.payby.com/ | `reader / reader_8Ssv8h2p2M6nBa` |
| mysql | mysql db | https://sqlquery.corp.payby.com/sqlquery/ | LDAP login |
| rabbit-mq | Message Queue | https://rabbitmq-admin.corp.payby.com/ | Readonly：`dev / dev@123` |
| spring-cloud-config | 配置中心 | 例：https://admin.corp.payby.com/gp008_acs/default | Developers 无修改权限；Azure 调用：`curl -u admin:admin https://admin.corp.payby.com/gp008_acs/default` |
| spring-boot-admin | SpringBoot 应用门户 | https://admin.corp.payby.com/springbootadmin/ | 仅 teamleader 有权限 |
| dubbo-admin | Dubbo 服务管理 | https://admin.corp.payby.com/dubbo-admin/ | API Invoke Forbidden；仅 teamleader 有权限 |
| elasticjob-console | 定时任务控制台 | https://admin.corp.payby.com/elasticjob-console/ | Readonly：`guest/guest`；仅 teamleader 有权限 |
| grafana - BUSINESS | 业务报表 | https://bi-dashboard.corp.algento.com/ | LDAP login |
| grafana - OPS | 性能报表 | https://monitor-soc.corp.payby.com/ | LDAP login；Redis 端口实例映射见 [[prod-env-access-guide#grafana-redis-端口映射]] |
| zookeeper | dubbo、elasticjob 配置中心 | `zk-cs.prod:2181` | UNI-JOB |
| redash | redash | https://redash.payby.com/ | — |
| Azure Cloud | WAF log 等 | https://portal.azure.com/ | 单独申请 |

## 业务 Portal (Business Portal)

| Portal | 说明 | URL |
|---|---|---|
| basis | Basis Portal | https://admin.corp.payby.com/basis/ |
| basis-cms | CMS Basis Portal | https://admin.corp.payby.com/basis-cms/ |
| basis-customer | Customer Basis Portal | https://admin.corp.payby.com/basis-customer/ |
| basis-merchant | Merchant Basis Portal | https://admin.corp.payby.com/basis-merchant/ |
| counter | C&S Portal | https://admin.corp.payby.com/counter/ |
| bigdata-admin | Risk Control Portal（反欺诈平台） | https://admin.corp.payby.com/bigdata-admin/ |
| merchant-console | Merchant Portal | https://b.payby.com/ |
| unified-merchant-portal | Unified Merchant Portal | https://unified.payby.com/ |
| bank-console | FAB Merchant Portal | https://cooperation-intra.payby.com |
| BMOC | Botim Money Operations Center | https://admin.corp.payby.com/bmoc/ |

## 其他门户 (Other Portal)

| Name | 说明 | URL |
|---|---|---|
| fidoService | 中间服务（机房内网） | http://cfca.payby.com ；http://fidoservice-svc |
| fidoRPAdapter | 演示服务（机房内网） | http://cfca.payby.com/RPAdapter/config.jsp |
| fidoMgmt | 管理平台 | https://admin.corp.payby.com/FidoMgmt/ |
| jollychic-service | jollychic 备胎 | https://api.payby.com/jollychic-service/swagger-ui.html |

## Grafana Redis 端口映射

业务域 `domain=payby-core-systems`，用于 Grafana - OPS 中按 Redis 实例查看监控。

| Domain | Grafana Port |
|---|---|
| redis.azure.payby.com | 6379 |
| redis-bigdata.azure.payby.com | 6380 |
| redis-token.azure.payby.com | 6381 |
| redis-bigdao.azure.payby.com | 6382 |
| redis-member.azure.payby.com | 6383 |
| redis-inf.azure.payby.com | 6384 |
| redis-risk.azure.payby.com | 6385 |
| redis-credit.azure.payby.com | 6386 |
| redis-remittance.azure.payby.com | 6387 |
