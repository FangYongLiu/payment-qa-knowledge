---
title: Merchant Portal MySQL连接信息
domain: authorization-protocol
kind: wiki_page
slug: merchant-portal-mysql-connection-info
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:ada86141-adb8-46be-b51a-f85653205ac0
tags: []
---

# Merchant Portal MySQL连接信息

本页记录商户控台 (Merchant Portal) 在 sim / dev / uat / stress 各环境下的 MySQL 连接地址与账号凭据，业务域为 `payby-authorization-protocol`。

## 连接地址 (mysql_uri)

| 环境 | mysql_uri |
|------|-----------|
| sim  | `dbfunc2.test2pay.com:3306` |
| dev  | `dbdev1.test2pay.com:3306` |
| uat  | `mysql-rds-uat-pby-aen-001.mysql.database.azure.com:3306`，SQL 查询入口：`https://sqlquery-uat.test2pay.com/sqlquery/` |
| stress | (StressDB 信息需向右滑动查看) |

## 账号凭据

每个环境提供多个账号，对应不同的访问场景。

### sim (dbfunc2 / dbfunc2.test2pay.com)

- `reader` / `reader_j0kqgaHxsI5O6j`
- `acsuser` / `acs_vVMcky7jFXdCLa`
- `cashdeskuser` / `cashdesk_UZXQgEpnL0mojh`

### dev (devdb1 / dbdev1.test2pay.com)

- `reader` / `reader_j0kqgaHxsI5O6j`
- `acsuser` / `acs_U7xVBvKA2ODFGn`
- `cashdeskuser` / (同列对应密码)

### uat (mysql-rds-uat-pby-aen-001)

- `reader` / `reader_kp...` (密码完整值见原表)
- `syncuser`
- `acsuser`

## 使用说明

- `reader` 账号支持查询所有数据库，仅具备**查询权限** (Only have query permission)，适合排查与验证场景。
- 第一列为 Username，第二列为 password；不同环境的同名账号 (例如 `acsuser`、`cashdeskuser`) 密码不同，切勿混用。
- uat 环境除直连 MySQL 外，还可通过 `sqlquery-uat.test2pay.com` 提供的 Web SQL 查询页面访问。
