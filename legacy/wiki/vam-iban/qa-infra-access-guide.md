---
title: QA基础设施访问指南(DB/Redis/Kibana)
domain: vam-iban
kind: wiki_page
slug: qa-infra-access-guide
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:f6158bcb-2259-47d0-87d4-ff82e274067c
tags: []
---

# QA基础设施访问指南(DB/Redis/Kibana)

本页汇总 QA 在 Sim/Uat/Prod 环境下访问数据库、Redis 与 Kibana 的连接信息与权限说明，便于测试时进行数据核对与日志排查。相关业务背景见 [[merchant-portal-overview]]，表级影响范围见 [[merchant-onboarding-database-scope]]。

## 数据库 (Database)

数据库连接配置参考 DBA 维护的密码文档：

- 配置地址：`http://gitlab.test2pay.com/dba/passwd/blob/master/mysql.md`
- 连接时需选择具体库名，例如 `merchantuser`

QA 数据库账号权限：

- `SELECT` – 查询数据
- `INSERT` – 插入数据
- `UPDATE` – 修改数据
- `DELETE` – 删除数据

涉及的核心库示例：`merchant`、`member`、`ppcenter`、`dpm`、`statementii`、`contract`、`vis`、`acquireii`、`mhtfundout`、`deposit`、`device` 等，具体表清单见 [[merchant-onboarding-database-scope]]。

## Redis 连接指南

| 环境 | Host | Port | 密码 |
|---|---|---|---|
| Sim (AWS) | `l-sim-lb-rediscluster-01-11f394e4e3d650f7.elb.me-central-1.amazonaws.com` | 6379 | `redis_skxnn6oLaTpKjh` |
| Uat (Azure) | `redis-cluster.uat-azure.test2pay.com` | 6379 | `redis_uat_gP6yxnvDGkQX7h` |

## Kibana 日志查询

| 环境 | URL | 账号/密码 |
|---|---|---|
| Sim | `https://sim-kibana.corp.test2pay.com/login?next=%2F` | 无需登录 |
| Uat | `https://uat-kibana.corp.test2pay.com/app/home` | `reader` / `reader@123` |
| Prod | `https://kibana.payby.com/app/home` | 1) 使用域账号登录；2) 系统账号 `reader` / `reader_Qwer` |

## 加解密查询 (PAYBY BASIS)

当数据库或日志中存储的是加密后的令牌（如 IBAN 持久化令牌）时，QA 可使用内部管理后台 PAYBY BASIS 进行加解密换算。

- 入口（Uat）：`https://uat.intra.test2pay.com/basis`
- 导航路径：`综合管理` → `功能查询` → `加解密查询`

页面提供四类加解密工具：

1. **临时令牌**：输入临时令牌，并指定有效时间（秒）。
2. **持久令牌**：输入持久令牌（含大字段）。
3. **批量持久令牌**：支持手工输入，也支持「从文件批量加密」/「从文件批量解密」。
4. **带摘要持久令牌**：选择数据类型（如 `iban`），输入明文与摘要后缀进行加解密。
   - 示例：数据类型 `iban`，明文 `AE27035741400060231020`，摘要 `1020`，加密结果形如 `P3194091-1020`。

左侧导航还包含：联合查询、密钥配置查询、UES证书、支付控制、补发通知、短链接、缓存清除、日志监控、数据配置、开放授权。

## 使用建议

- 测试 Onboarding 流程时，结合 [[flow_merchant_onboarding]] 与 [[merchant-onboarding-database-scope]] 定位影响表。
- 排查收单链路问题（产品申请、交易、账户、对账单、离线设备等）参考 [[acquire-merchant-console]] 与 [[scn_acquire_product_apply]]。
- 服务应用与 Owner 对照见 [[merchant-portal-service-components]]。
- 涉及 IBAN 等敏感字段在 DB / Kibana 中以密文存储时，使用上文 PAYBY BASIS 的「带摘要持久令牌」工具完成明文 ↔ 密文换算。
