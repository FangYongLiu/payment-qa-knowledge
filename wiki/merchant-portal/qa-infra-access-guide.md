---
title: QA基础设施访问指南(DB/Redis/Kibana)
domain: merchant-portal
kind: wiki_page
slug: qa-infra-access-guide
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:PMDPayment/124554596
tags: []
---

# QA基础设施访问指南(DB/Redis/Kibana)

本页汇总 QA 在 Sim/Uat/Prod 环境下访问数据库、Redis 与 Kibana 的连接信息与权限说明，便于测试时进行数据核对与日志排查。相关业务背景见 [[merchant-portal-overview]]，表级影响范围见 [[merchant-onboarding-database-scope]]。Prod 环境的门户与工具入口另见 [[prod-env-portal-access-guide]]。

## 数据库 (Database)

### Sim / Uat 环境

数据库连接配置参考 DBA 维护的密码文档：

- 配置地址：`http://gitlab.test2pay.com/dba/passwd/blob/master/mysql.md`
- 连接时需选择具体库名，例如 `merchantuser`

QA 数据库账号权限：

- `SELECT` – 查询数据
- `INSERT` – 插入数据
- `UPDATE` – 修改数据
- `DELETE` – 删除数据

涉及的核心库示例：`merchant`、`member`、`ppcenter`、`dpm`、`statementii`、`contract`、`vis`、`acquireii`、`mhtfundout`、`deposit`、`device` 等，具体表清单见 [[merchant-onboarding-database-scope]]。

### Prod 环境

通过统一 SQL 查询入口访问：

- URL：`https://sqlquery.corp.payby.com/sqlquery/`
- 登录方式：LDAP 登录

## Redis 连接指南

### Sim / Uat 环境

| 环境 | Host | Port | 密码 |
|---|---|---|---|
| Sim (AWS) | `l-sim-lb-rediscluster-01-11f394e4e3d650f7.elb.me-central-1.amazonaws.com` | 6379 | `redis_skxnn6oLaTpKjh` |
| Uat (Azure) | `redis-cluster.uat-azure.test2pay.com` | 6379 | `redis_uat_gP6yxnvDGkQX7h` |

### Prod 环境 Redis 实例 (Grafana 端口映射)

Prod Redis 通过 Grafana 监控暴露不同实例，按域名区分用途：

| Domain | Port |
|---|---|
| `redis.azure.payby.com` | 6379 |
| `redis-bigdata.azure.payby.com` | 6380 |
| `redis-token.azure.payby.com` | 6381 |
| `redis-bigdao.azure.payby.com` | 6382 |
| `redis-member.azure.payby.com` | 6383 |
| `redis-inf.azure.payby.com` | 6384 |
| `redis-risk.azure.payby.com` | 6385 |
| `redis-credit.azure.payby.com` | 6386 |
| `redis-remittance.azure.payby.com` | 6387 |

Grafana OPS 入口：`https://monitor-soc.corp.payby.com/`（LDAP 登录）。

## Kibana 日志查询

### 环境入口

| 环境 | URL | 账号/密码 |
|---|---|---|
| Sim | `https://sim-kibana.corp.test2pay.com/login?next=%2F` | 无需登录 |
| Uat | `https://uat-kibana.corp.test2pay.com/app/home` | `reader` / `reader@123` |
| Prod (App Log) | `https://kibana.corp.payby.com/` | Azure：`reader` / `reader_Qwer`；cgs/sgs 用户：`porter_user`；app_log 用户：`app_log_user` |
| Prod (Business) | `https://esdata-kibana.corp.payby.com/` | `reader` / `reader_8Ssv8h2p2M6nBa` |

### Prod Kibana 索引说明

- `java-logstash-*` — ANALYSIS（应用日志）
- `porter_cgs*` — ANALYSIS（cgs 渠道）
- `porter_sgs*` — ANALYSIS（sgs 渠道）

Prod 环境同时提供历史入口 `https://kibana.payby.com/app/home`：
1. 使用域账号登录；
2. 系统账号 `reader` / `reader_Qwer`。

## Prod 环境其他基础设施

完整的 Prod 门户与工具清单见 [[prod-env-portal-access-guide]]，常用入口摘录：

| 工具 | 用途 | URL | 访问方式 |
|---|---|---|---|
| Alhambra (appcenter) | k8s portal | `https://appcenter.corp.payby.com/` | — |
| Skywalking | APM | `https://skw.corp.payby.com/` | — |
| RabbitMQ Admin | 消息队列管理 | `https://rabbitmq-admin.corp.payby.com/` | 只读：`dev` / `dev@123` |
| Spring Cloud Config | 配置中心 | 例：`https://admin.corp.payby.com/gp008_acs/default` | `curl -u admin:admin ...` |
| Spring Boot Admin | 应用门户 | `https://admin.corp.payby.com/springbootadmin/` | 仅 teamleader |
| Dubbo Admin | Dubbo 服务管理 | `https://admin.corp.payby.com/dubbo-admin/` | 仅 teamleader，API 调用禁用 |
| Elasticjob Console | 定时任务控制台 | `https://admin.corp.payby.com/elasticjob-console/` | 只读：`guest` / `guest` |
| Grafana - Business | 业务报表 | `https://bi-dashboard.corp.algento.com/` | LDAP |
| Grafana - OPS | 性能报表 | `https://monitor-soc.corp.payby.com/` | LDAP |
| Zookeeper | dubbo / elasticjob 配置中心 | `zk-cs.prod:2181` | — |
| Redash | 数据查询 | `https://redash.payby.com/` | — |
| Azure Cloud | WAF log 等 | `https://portal.azure.com/` | 单独申请 |

## 使用建议

- 测试 Onboarding 流程时，结合 [[flow_merchant_onboarding]] 与 [[merchant-onboarding-database-scope]] 定位影响表。
- 排查收单链路问题（产品申请、交易、账户、对账单、离线设备等）参考 [[acquire-merchant-console]] 与 [[scn_acquire_product_apply]]。
- 服务应用与 Owner 对照见 [[merchant-portal-service-components]]。
- Prod 环境涉及生产数据访问，敏感操作前先确认权限范围；门户清单与登录方式详见 [[prod-env-portal-access-guide]]。
