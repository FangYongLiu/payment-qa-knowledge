---
title: PROD环境门户与工具访问指南
domain: merchant-portal
kind: wiki_page
slug: prod-env-portal-access-guide
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:PMDPayment/124554596
tags: []
---

# PROD环境门户与工具访问指南

本页汇总 PROD 环境下业务门户（Basis / Merchant / BMOC 等）及配套工具/中间件的访问入口与登录方式，便于 QA 在生产环境进行业务核查与问题定位。基础设施访问可参见 [[qa-infra-access-guide]]。

## 业务门户 (Business Portal)

| Portal | 描述 | URL |
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

## 其它业务服务 (Other Portal)

- **fidoService**（中间服务，机房内网）：`http://cfca.payby.com`、`http://fidoservice-svc`
- **fidoRPAdapter**（演示服务，机房内网）：`http://cfca.payby.com/RPAdapter/config.jsp`
- **fidoMgmt**（管理平台）：https://admin.corp.payby.com/FidoMgmt/
- **jollychic-service**（jollychic 备胎）：https://api.payby.com/jollychic-service/swagger-ui.html

## 平台与运维工具

- **Alhambra / appcenter**（k8s portal）：https://appcenter.corp.payby.com/
- **skywalking**（APM）：https://skw.corp.payby.com/
- **spring-cloud-config**（配置中心，开发者无修改权限）：示例 `https://admin.corp.payby.com/gp008_acs/default`，Azure 拉取：`curl -u admin:admin https://admin.corp.payby.com/gp008_acs/default`
- **spring-boot-admin**：https://admin.corp.payby.com/springbootadmin/ （仅 teamleader）
- **dubbo-admin**（dubbo 服务管理）：https://admin.corp.payby.com/dubbo-admin/ （API Invoke Forbidden，仅 teamleader）
- **elasticjob-console**（定时任务控制台）：https://admin.corp.payby.com/elasticjob-console/ ，只读 `guest/guest`，仅 teamleader
- **rabbit-mq**：https://rabbitmq-admin.corp.payby.com/ ，只读 `dev / dev@123`
- **zookeeper**（dubbo、elasticjob 配置中心）：`zk-cs.prod:2181`，UNI-JOB
- **Azure Cloud**（WAF log 等）：https://portal.azure.com/ （单独申请权限）

## 数据查询与报表

- **Log Kibana**（es7 日志）：https://kibana.corp.payby.com/
  - 索引：`java-logstash-*`(ANALYSIS)、`porter_cgs*`(ANALYSIS)、`porter_sgs*`(ANALYSIS)
  - 账号：Azure `reader / reader_Qwer`；cgs/sgs 用户 `porter_user`；app_log 用户 `app_log_user`
- **Business Kibana**（es7 业务数据）：https://esdata-kibana.corp.payby.com/ ，`reader / reader_8Ssv8h2p2M6nBa`
- **mysql**（DB 查询）：https://sqlquery.corp.payby.com/sqlquery/ ，LDAP 登录
- **grafana - BUSINESS**（业务报表）：https://bi-dashboard.corp.algento.com/ ，LDAP 登录
- **grafana - OPS**（性能报表）：https://monitor-soc.corp.payby.com/ ，LDAP 登录
- **redash**：https://redash.payby.com/

## 附录：Grafana Redis 端口映射

OPS Grafana 中按下表 Port 区分各 Redis 实例：

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
