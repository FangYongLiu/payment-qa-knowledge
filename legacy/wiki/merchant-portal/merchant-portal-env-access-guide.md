---
title: 环境访问与基础设施指南(DB/Redis/Kibana)
domain: merchant-portal
kind: wiki_page
slug: merchant-portal-env-access-guide
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/997785804
tags: []
---

# 环境访问与基础设施指南(DB/Redis/Kibana)

本页汇总 Merchant Portal 业务域在 SIM / UAT / Prod 环境下的数据库、Redis、Kibana 连接方式与账号信息，便于 QA 在测试与排障时快速访问基础设施。

## 商户控台前端访问入口

| 环境 | 访问地址 | 测试账号 |
|---|---|---|
| Sim | https://sim-web-unified.test2pay.com/verify/login | Mobile: `+971-556579167`<br>Password: `132580` 或 `Yong0324####`<br>OTP: `161616` (默认)<br>Choose Merchant: `SimBasisMerchant0628` |
| Uat | https://uat-web-unified.test2pay.com/verify/login | Mobile: `+971-556579167`<br>Password: `132580` 或 `Yong0324####`<br>OTP: real otp |

说明：
- 首次注册默认走 OTP 登录，登录后需设置密码。
- SIM 环境默认 OTP 固定为 `161616`；UAT 环境需要真实 OTP。
- 控台功能与业务流程见 [[merchant-portal-overview]]、[[acquire-merchant-console-guide]]。

## 数据库连接

### 连接配置
- 配置文档(DBA 维护)：`http://gitlab.test2pay.com/dba/passwd/blob/master/mysql.md`
- 连接时需指定具体 database name，例如 `merchantuser`。

### QA 账号权限
- `SELECT` – 查询数据
- `INSERT` – 插入数据
- `UPDATE` – 修改数据
- `DELETE` – 删除数据

### 涉及的库
商户入驻及控台相关数据库主要包括：`merchant`、`member`、`ppcenter`、`dpm`、`statementii`、`contract`、`vis`、`acquireii`、`mhtfundout`、`deposit`、`device`。

具体表与影响范围参考 [[merchant-onboarding-database-scope]]。

## Redis 连接

| 环境 | Host | Port | 密码 |
|---|---|---|---|
| Sim (AWS) | `l-sim-lb-rediscluster-01-11f394e4e3d650f7.elb.me-central-1.amazonaws.com` | 6379 | `redis_skxnn6oLaTpKjh` |
| Uat (Azure) | `redis-cluster.uat-azure.test2pay.com` | 6379 | `redis_uat_gP6yxnvDGkQX7h` |

## Kibana 日志查询

| 环境 | URL | 账号 / 密码 |
|---|---|---|
| Sim | https://sim-kibana.corp.test2pay.com/login?next=%2F | 无需登录 |
| Uat | https://uat-kibana.corp.test2pay.com/app/home | `reader` / `reader@123` |
| Prod | https://kibana.payby.com/app/home | 1. 使用域账号登录<br>2. 系统账号 `reader` / `reader_Qwer` |

## BMOC 后台入口(配套)

商户入驻后的审核入口(SIM)：
`https://sim-admin.corp.test2pay.com/basis-cas/login?service=https://sim-admin.corp.test2pay.com/bmoc/cas`

- 菜单：`Basis Merchant => Business => Merchant => Merchant Onboarding`
- 用于完成 AML Risk Calculate 与 KYB Approval；详细流程见 [[flow_merchant_onboarding]]。

## 相关页面
- 服务组件与 Owner 清单：[[merchant-onboarding-service-map]]
- 商户入驻数据落库范围：[[merchant-onboarding-database-scope]]
- 收单产品申请与审核：[[flow_acquire_product_application]]
