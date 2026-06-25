---
id: ref_portal_env_access
object_type: reference
name: 门户/运营环境访问指南(DB/Redis/Kibana/门户/k8s)
aliases: [env access guide, 环境访问, qa infra access, uat access, prod access]
domain: portal-operations
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: 'confluence:PMDPayment/124554687, PMDPayment/124554596, AQ/997785804, wiki:8031f2d2'
tags: [environment, access, database, redis, kibana, k8s, portal, sim, uat, prod]
related_services: [svc_unified_merchant_portal, svc_basis_merchant]
---

# 门户/运营环境访问指南(DB/Redis/Kibana/门户/k8s)

> QA 在 Sim/UAT/Prod 环境下访问商户门户、内部后台、数据库、Redis、Kibana 及基础设施的统一索引。敏感操作(尤其 Prod)前先确认权限范围。

## 商户门户前端入口与测试账号
| 环境 | 地址 | 测试账号 / OTP |
| --- | --- | --- |
| Sim | https://sim-web-unified.test2pay.com/verify/login | Mobile `+971-556579167` / Password `132580` 或 `Yong0324####` / OTP 默认 `161616` / Choose Merchant `SimBasisMerchant0628` |
| UAT | https://uat-web-unified.test2pay.com/verify/login | 同上账号，OTP 需 real OTP |
| Prod(merchant-console) | https://b.payby.com/ ；https://unified.payby.com/ | Merchant 账号 |
| Bank 控台(Sim) | https://sim-cooperation.test2pay.com/ | `can.wang@payby.com` / `1qaz!QAZ`(定制化控台，账号体系独立) |

首次注册默认 OTP 登录，登录后必须设置密码。

## Inner Portal(内部后台)
| 应用 | 说明 | UAT 地址 | Prod 地址 | 登录 |
| --- | --- | --- | --- | --- |
| basis | 业务运营后台 | http://uat.intra.azure.test2pay.com/basis/ | https://admin.corp.payby.com/basis/ | LDAP |
| basis-cms | CMS | http://uat.intra.azure.test2pay.com/basis-cms/ | https://admin.corp.payby.com/basis-cms/ | LDAP |
| basis-merchant | Basis Merchant | http://uat.intra.azure.test2pay.com/basis-merchant | https://admin.corp.payby.com/basis-merchant/ | LDAP |
| basis-customer | 客服系统 | http://uat-admin.azure.test2pay.com/basis-customer/login | https://admin.corp.payby.com/basis-customer/ | LDAP / User Name |
| counter | 资金管理后台 | http://uat.intra.azure.test2pay.com/counter/ | https://admin.corp.payby.com/counter/ | LDAP |
| BMOC | Botim Money Operations Center | https://uat-admin.corp.test2pay.com/bmoc/ | https://admin.corp.payby.com/bmoc/ | LDAP(员工域账号) |
| bank-console | FAB Merchant Portal | — | https://cooperation-intra.payby.com | — |
| bigdata-admin | 风控/反欺诈平台 | — | https://admin.corp.payby.com/bigdata-admin/ | LDAP |

BMOC 登录需员工域账号(账号问题找 OPS: wei.li)，登录后由 QA 添加角色权限。入驻审核入口(Sim):`https://sim-admin.corp.test2pay.com/basis-cas/login?service=https://sim-admin.corp.test2pay.com/bmoc/cas`，菜单 `Basis Merchant => Business => Merchant => Merchant Onboarding`(AML Risk Calculate + KYB Approval)。

## 数据库(Database)
- 连接配置(DBA 维护):`http://gitlab.test2pay.com/dba/passwd/blob/master/mysql.md`，连接需选具体库名(如 `merchantuser`)。
- Prod 统一查询入口:`https://sqlquery.corp.payby.com/sqlquery/`(LDAP)。
- QA 账号权限:SELECT / INSERT / UPDATE / DELETE。
- 商户门户相关核心库:`merchant`、`member`、`ppcenter`、`dpm`、`statementii`、`contract`、`vis`、`acquireii`、`mhtfundout`、`deposit`、`device`。

## Redis
| 环境 | Host | Port | 密码 |
| --- | --- | --- | --- |
| Sim(AWS) | `l-sim-lb-rediscluster-01-11f394e4e3d650f7.elb.me-central-1.amazonaws.com` | 6379 | `redis_skxnn6oLaTpKjh` |
| UAT(Azure) | `redis-cluster.uat-azure.test2pay.com` | 6379 | `redis_uat_gP6yxnvDGkQX7h` |
| UAT(老地址) | `10.91.11.79` | 6379 | `redis@Payby` |

Prod Redis 通过 Grafana(`https://monitor-soc.corp.payby.com/`，LDAP)按端口区分实例:6379 redis、6380 bigdata、6381 token、6382 bigdao、6383 member、6384 inf、6385 risk、6386 credit、6387 remittance(`redis*.azure.payby.com`)。

## Kibana 日志
| 环境 | URL | 账号 |
| --- | --- | --- |
| Sim | https://sim-kibana.corp.test2pay.com/ | 无需登录 |
| UAT | https://uat-kibana.corp.test2pay.com/app/home | `reader` / `reader@123`(另有 `reader/reader`);cgs/sgs 用户 `porter_user`;app_log 用户 `app_log_user` |
| UAT Business | uat-esdata-kibana-azure.test2pay.com | `reader` / `reader_NEpkhu3kzzXXRn` |
| Prod App Log | https://kibana.corp.payby.com/ | Azure `reader`/`reader_Qwer`;cgs/sgs `porter_user`;app_log `app_log_user` |
| Prod Business | https://esdata-kibana.corp.payby.com/ | `reader` / `reader_8Ssv8h2p2M6nBa` |

Prod 索引:`java-logstash-*`(应用日志 ANALYSIS)、`porter_cgs*`(cgs 渠道)、`porter_sgs*`(sgs 渠道)。

## 基础设施与运维工具
| 工具 | 用途 | UAT | Prod |
| --- | --- | --- | --- |
| Alhambra(appcenter) | k8s portal | https://appcenter.corp.payby.com/ | https://appcenter.corp.payby.com/ |
| skywalking | APM/调用链 | Azure http://10.33.0.10:30605 | https://skw.corp.payby.com/ |
| nacos | 应用发现 | http://uat.intra.azure.test2pay.com/nacos(nacos/nacos) | — |
| rabbit-mq | 消息中间件 | https://uat-rabbitmq-admin.corp.test2pay.com/(admin/admin@Payby) | https://rabbitmq-admin.corp.payby.com/(只读 dev/dev@123) |
| spring-cloud-config | 配置中心 | uat.config.test2pay.com / uat.config.azure.test2pay.com(admin/admin) | admin.corp.payby.com/<app>/default |
| spring-boot-admin | 应用管理 | http://uat.intra.azure.test2pay.com/springbootadmin/(admin/admin123) | 仅 teamleader |
| dubbo-admin | dubbo 管理 | http://uat.intra.azure.test2pay.com/dubbo-admin/ | 仅 teamleader(调用禁用) |
| elasticjob-console | 定时任务 | http://uat.intra.azure.test2pay.com/elasticjob-console/(admin/admin123) | 只读 guest/guest |
| zookeeper | 服务发现 | nodeservice.g42pay.com:32181 | zk-cs.prod:2181 |
| mysql | DB 直连 | rds1.uat.test2pay.com / elb-rds1.uat.test2pay.com | sqlquery 入口 |
| mongo | 主库 | mongodb1/2.uat-azure.test2pay.com:8635 | — |
| grafana(BI) | 业务报表 | uat-monitor-soc.test2pay.com(LDAP) | bi-dashboard.corp.algento.com / monitor-soc.corp.payby.com(LDAP) |
| redash | 数据查询 | — | https://redash.payby.com/ |

### spring-cloud-config 拉取示例
```
curl -u admin:admin http://uat.config.test2pay.com/gp008_acs/uat        # G42
curl -u admin:admin http://uat.config.azure.test2pay.com/gp008_acs/uat  # Azure
```

### k8s(kubectl)常用命令
```
kubectl --kubeconfig ~/.kube/uat-config-azure -n uat get pods --sort-by=.status.startTime
kubectl --kubeconfig /root/.kube/uat-config -n uat exec -it <pod> -- /bin/bash
kubectl --kubeconfig /root/.kube/uat-config -n uat describe pod <pod>
kubectl --kubeconfig /root/.kube/uat-config -n uat -o wide get svc
kubectl --kubeconfig /root/.kube/uat-config -n uat cp <pod>:/tmp/<file> <file>
```
日志服务器:`localadmin/localadmin` 登录 `10.90.15.171`。

## UAT Maven settings.xml(开发构建)
- 私服统一指向 `http://10.90.15.141:8181`(外网不可达);激活 profile `development`。
- 部署认证 server `deployRelease`/`deploySnapshot` 均 `dev/dev`。
- `internal` 仓库 release `updatePolicy=never`、snapshot `always`;`deployRelease`/`deploySnapshot` 分别只启用 release/snapshot。
- 切换环境需替换所有 `servers` 与 `repository`/`pluginRepository` URL;Maven 按 `distributionManagement` 的 id 匹配 `servers` 取认证。

## 其它入口
- Vendor Portal fidoMgmt:UAT `https://uat-admin.corp.test2pay.com/FidoMgmt/...`(admin/admin123);Prod `https://admin.corp.payby.com/FidoMgmt/`。
- 支付通知 pns:`http://intra.g42pay.com/pns/services`。
- 关联流程:入驻 [[flow_merchant_onboarding]]、产品申请 [[flow_acquire_product_application]];后台菜单 [[ref_bmoc_basis_merchant]]。
