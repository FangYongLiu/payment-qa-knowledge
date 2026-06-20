---
title: AE UAT环境访问指南(基础设施与门户)
domain: merchant-portal
kind: wiki_page
slug: env-uat-ae-access-guide
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:PMDPayment/124554687
tags: []
---

# AE UAT环境访问指南(基础设施与门户)

本页汇总 AE 商户联调 UAT 环境（ENV-UAT）下基础设施组件、内外门户、支付应用与 Vendor Portal 的访问地址、账号及常用命令示例，便于联调与排查时快速定位入口。

## 适用范围

- 环境：AE-b-商户联调环境(UAT)
- 公共地址族：a公共地址
- 迁移信息：Migrated to ENV-UAT

## 基础设施

| 应用名称 | 说明 | 服务地址 / 管理后台 | 账号/备注 |
|---|---|---|---|
| Alhambra (appcenter) | k8s portal | https://appcenter.corp.payby.com/ | - |
| skywalking | 性能监控，调用链 | Azure: http://10.33.0.10:30605 | - |
| nacos | springboot应用发现 | Azure: http://uat.intra.azure.test2pay.com/nacos | nacos/nacos |
| rabbit-mq | 消息中间件 | new: https://uat-rabbitmq-admin.corp.test2pay.com/ ; Bind Host: 10.32.231.254 | admin/admin@Payby |
| spring-cloud-config | 配置中心 | Azure: http://gitlab.test2pay.com/uat/config_uat-azure/ ; G42: uat.config.test2pay.com ; Azure: uat.config.azure.test2pay.com | 见下方 curl 示例 |
| spring-boot-admin | springboot应用管理 | Azure: http://uat.intra.azure.test2pay.com/springbootadmin/ | admin/admin123 |
| dubbo-admin | dubbo服务管理 | Azure: http://uat.intra.azure.test2pay.com/dubbo-admin/ | - |
| dubbo nodeservice | dubbo | uat.nodeservice.test2pay.com 或 uat-nodeservice-azure.test2pay.com | - |
| elasticjob-console | 定时任务管理后台 | Azure: http://uat.intra.azure.test2pay.com/elasticjob-console/ | admin/admin123 |
| Log Kibana | Log data in es7 | https://uat-kibana.corp.test2pay.com/ | reader/reader；cgs,sgs user: porter_user；app_log user: app_log_user |
| Business kibana | Business data in es7 | G42 & Azure: uat-esdata-kibana-azure.test2pay.com | reader/reader_NEpkhu3kzzXXRn |
| redis | 缓存服务 | 10.91.11.79:6379 | redis@Payby |
| k8s | k8s | uat-az 或 uat-azure | 见下方 kubectl 示例 |
| grafana | 服务监控 | Azure: uat-monitor-soc.test2pay.com | LDAP Login |
| zookeeper | 服务发现 | nodeservice.g42pay.com:32181 | - |
| mysql | mysql | G42: rds1.uat.test2pay.com ；Migrate ELB: elb-rds1.uat.test2pay.com | - |
| mongo主库 | uat mongo主库 | mongodb1.uat-azure.test2pay.com:8635 ；mongodb2.uat-azure.test2pay.com:8635 | - |

### spring-cloud-config 拉取示例

```
# G42
curl -u admin:admin http://uat.config.test2pay.com/gp008_acs/uat
# Azure
curl -u admin:admin http://uat.config.azure.test2pay.com/gp008_acs/uat
```

### k8s (kubectl) 常用命令

- 通用形式：`kubectl --kubeconfig ~/.kube/uat-config-azure -n uat arg1 arg2`
- 按启动时间列出 Pod：

```
kubectl --kubeconfig ~/.kube/uat-config-azure -n uat get pods --sort-by=.status.startTime
```

- 进入 Pod / 描述 Pod / 查看 svc：

```
kubectl --kubeconfig /root/.kube/uat-config -n uat exec -it acs-587d949d75-8s5n2 -- /bin/bash
kubectl --kubeconfig /root/.kube/uat-config -n uat describe pod acs-587d949d75-8s5n2
kubectl --kubeconfig /root/.kube/uat-config -n uat -o wide get svc
```

- 从 Pod 拷贝文件：

```
kubectl --kubeconfig /root/.kube/uat-config -n uat cp \
  feebill-8fb9ccdd5-tzq9f:/tmp/FEE_BILL_343cffd7c6734e80a776eaae18f1fa4e8153543168792915072.html \
  FEE_BILL_343cffd7c6734e80a776eaae18f1fa4e8153543168792915072.html
```

### 日志服务器登录

- 用 `localadmin` 用户登录 `10.90.15.171`
- log服务器换账号登陆：`localadmin/localadmin`

## Inner Portal（内部门户）

| 应用名称 | 说明 | 访问地址 | Memo |
|---|---|---|---|
| basis | 业务运营后台 | http://uat.intra.azure.test2pay.com/basis/ | LDAP |
| basis-cms | cms | http://uat.intra.azure.test2pay.com/basis-cms/ | LDAP |
| basis-merchant | Basis Merchant | http://uat.intra.azure.test2pay.com/basis-merchant | LDAP |
| counter | 资金管理后台 | http://uat.intra.azure.test2pay.com/counter/ | LDAP |
| basis-customer | 客服系统 | http://uat-admin.azure.test2pay.com/basis-customer/login | LDAP or User Name |
| BMOC | Botim Money Operations Center | https://uat-admin.corp.test2pay.com/bmoc/ | LDAP |

## Outer Portal（外部门户）

| 应用名称 | 说明 | 访问地址 | Memo |
|---|---|---|---|
| merchant | 商户后台 | https://uat-web-merchant.test2pay.com/login | Merchant |

## 支付应用

| 应用名称 | 说明 | 访问地址 |
|---|---|---|
| pns | 商户/合作方通知 | http://intra.g42pay.com/pns/services |

## Vendor Portal

| 应用名称 | 说明 | 访问地址 | 账号 |
|---|---|---|---|
| fidoMgmt | 管理平台 | https://uat-admin.corp.test2pay.com/FidoMgmt/login/login.do | admin/admin123 |

## Reference

- DBA：数据库 sim/uat/dev/stress 地址（详见 DBA 资源）
