---
id: tbl_devicefpii_app
object_type: Table
name: 应用表 (app)
aliases: [app, devicefpii.app]
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: devicefpii schema DDL
tags: [risk, devicefpii]
sensitivity: normal
related_services: []
---

# 应用表 (app)

## 用途
物理表 `devicefpii.app`,主键 `Id`。应用表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | app · 可空 |
| `name` | varchar(255) | app |
| `description` | varchar(255) | 待补 |
| `app_key` | varchar(255) | 待补 |
| `app_secret` | varchar(255) | app |
| `create_time` | timestamp | 待补 |
| `modify_time` | timestamp | 待补 |
| `package_name` | varchar(512) | 待补 · 可空 |
| `Id` | int unsigned | 主键 · 可空 |
| `AppId` | varchar(64) | AppID |
| `Name` | varchar(500) | 应用名 |
| `OrgId` | varchar(32) | 部门Id |
| `OrgName` | varchar(64) | 部门名字 |
| `OwnerName` | varchar(500) | ownerName |
| `OwnerEmail` | varchar(500) | ownerEmail |
| `IsDeleted` | bit | 1: deleted, 0: normal |
| `DeletedAt` | bigint | Delete timestamp based on milliseconds |
| `DataChange_CreatedBy` | varchar(64) | 创建人邮箱前缀 |
| `DataChange_CreatedTime` | timestamp | 创建时间 |
| `DataChange_LastModifiedBy` | varchar(64) | 最后修改人邮箱前缀 · 可空 |
| `DataChange_LastTime` | timestamp | 最后修改时间 · 可空 |

## 主键 / 索引
- 主键:`Id`
- `un_app_key`:app_key (UNIQUE)
- `UK_AppId_DeletedAt`:AppId, DeletedAt (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
