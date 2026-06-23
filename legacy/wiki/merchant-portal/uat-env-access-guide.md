---
title: UAT环境访问与基础设施指南
domain: merchant-portal
kind: wiki_page
slug: uat-env-access-guide
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:8031f2d2-cdc0-4eb9-b051-dd466a2d41bd
tags: []
---

# UAT环境访问与基础设施指南

本页汇总 AE-b 商户联调环境（UAT）下，基础设施、内部后台、商户后台、支付应用及 Vendor Portal 的访问地址、登录凭证与常用命令。

## 基础设施

| 应用 | 说明 | 地址 | 凭证 |
|---|---|---|---|
| Alhambra (appcenter) | k8s portal | https://appcenter.corp.payby.com/ | - |
| skywalking | 性能监控、调用链 | Azure: http://10.33.0.10:30605 | - |
| nacos | springboot 应用发现 | Azure: http://uat.intra.azure.test2pay.com/nacos | nacos/nacos |
| rabbit-mq | 消息中间件 | new: https://uat-rabbitmq-admin.corp.test2pay.com/ ；Bind Host: 10.32.231.254 | admin/admin@Payby |
| spring-cloud-config | 配置中心 | Azure: http://gitlab.test2pay.com/uat/config_uat-azure/ ；G42: uat.config.test2pay.com ；Azure: uat.config.azure.test2pay.com | admin/admin |
| spring-boot-admin | springboot 应用管理 | Azure: http://uat.intra.azure.test2pay.com/springbootadmin/ | admin/admin123 |
| dubbo-admin | dubbo 服务管理 | Azure: http://uat.intra.azure.test2pay.com/dubbo-admin/ | - |
| dubbo nodeservice | dubbo | uat.nodeservice.test2pay.com 或 uat-nodeservice-azure.test2pay.com | - |
| elasticjob-console | 定时任务管理后台 | Azure: http://uat.intra.azure.test2pay.com/elasticjob-console/ | admin/admin123 |
| Log Kibana | Log data in es7 | https://uat-kibana.corp.test2pay.com/ | reader/reader；cgs,sgs: porter_user；app_log: app_log_user |
| Business Kibana | Business data in es7 | G42 & Azure: uat-esdata-kibana-azure.test2pay.com | reader/reader_NEpkhu3kzzXXRn |
| redis | 缓存服务 | 10.91.11.79:6379 | redis@Payby |
| grafana | 服务监控 | Azure: uat-monitor-soc.test2pay.com | LDAP Login |
| zookeeper | 服务发现 | nodeservice.g42pay.com:32181 | - |
| mysql | mysql | G42: rds1.uat.test2pay.com ；Migrate ELB: elb-rds1.uat.test2pay.com | - |
| mongo 主库 | UAT mongo 主库 | mongodb1.uat-azure.test2pay.com:8635 ；mongodb2.uat-azure.test2pay.com:8635 | - |

## k8s 常用命令

集群标识：`uat-az` 或 `uat-azure`，Azure 使用 kubeconfig `~/.kube/uat-config-azure`，namespace `uat`。

- 列出 Pod（按启动时间排序）：
  ```
  kubectl --kubeconfig ~/.kube/uat-config-azure -n uat get pods --sort-by=.status.startTime
  ```
- 进入容器：
  ```
  kubectl --kubeconfig /root/.kube/uat-config -n uat exec -it acs-587d949d75-8s5n2 -- /bin/bash
  ```
- 查看 Pod 详情：
  ```
  kubectl --kubeconfig /root/.kube/uat-config -n uat describe pod acs-587d949d75-8s5n2
  ```
- 查看 Service：
  ```
  kubectl --kubeconfig /root/.kube/uat-config -n uat -o wide get svc
  ```
- 从容器拷贝文件：
  ```
  kubectl --kubeconfig /root/.kube/uat-config -n uat cp feebill-8fb9ccdd5-tzq9f:/tmp/FEE_BILL_xxx.html FEE_BILL_xxx.html
  ```

> 日志服务器：使用 `localadmin/localadmin` 登录 `10.90.15.171`。

## spring-cloud-config 拉取配置

- G42：`curl -u admin:admin http://uat.config.test2pay.com/gp008_acs/uat`
- Azure：`curl -u admin:admin http://uat.config.azure.test2pay.com/gp008_acs/uat`

## Inner Portal（内部后台）

| 应用 | 说明 | 地址 | 登录方式 |
|---|---|---|---|
| basis | 业务运营后台 | http://uat.intra.azure.test2pay.com/basis/ | LDAP |
| basis-cms | CMS | http://uat.intra.azure.test2pay.com/basis-cms/ | LDAP |
| basis-merchant | Basis Merchant | http://uat.intra.azure.test2pay.com/basis-merchant | LDAP |
| counter | 资金管理后台 | http://uat.intra.azure.test2pay.com/counter/ | LDAP |
| basis-customer | 客服系统 | http://uat-admin.azure.test2pay.com/basis-customer/login | LDAP 或 User Name |
| BMOC | Botim Money Operations Center | https://uat-admin.corp.test2pay.com/bmoc/ | LDAP |

## Outer Portal（商户后台）

| 应用 | 说明 | 地址 | 登录方式 |
|---|---|---|---|
| merchant | 商户后台 | https://uat-web-merchant.test2pay.com/login | Merchant 账号 |

## 支付应用

| 应用 | 说明 | 地址 |
|---|---|---|
| pns | 商户/合作方通知 | http://intra.g42pay.com/pns/services |

## Vendor Portal

| 应用 | 说明 | 地址 | 凭证 |
|---|---|---|---|
| fidoMgmt | 管理平台 | https://uat-admin.corp.test2pay.com/FidoMgmt/login/login.do | admin/admin123 |

## 参考

- 数据库 sim/uat/dev/stress 地址由 DBA 维护。
