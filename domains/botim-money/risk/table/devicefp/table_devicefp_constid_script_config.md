---
id: tbl_devicefp_constid_script_config
object_type: Table
name: 开放API消费者 (constid_script_config)
aliases: [constid_script_config, devicefp.constid_script_config]
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: devicefp schema DDL
tags: [risk, devicefp]
sensitivity: normal
related_services: []
---

# 开放API消费者 (constid_script_config)

## 用途
物理表 `devicefp.constid_script_config`,主键 `Id`。开放API消费者。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 待补 · 可空 |
| `name` | varchar(255) | 待补 |
| `enable_flag` | tinyint | 待补 |
| `default_flag` | tinyint | 待补 |
| `type` | tinyint(6) | 待补 |
| `test_script` | text | 待补 · 可空 |
| `file_name` | varchar(255) | 待补 · 可空 |
| `description` | varchar(128) | 待补 · 可空 |
| `create_time` | datetime | 待补 |
| `modify_time` | datetime | 待补 · 可空 |
| `id` | int | 待补 · 可空 |
| `config_id` | int | 待补 |
| `script` | text | 待补 · 可空 |
| `choose_field` | text | 待补 · 可空 |
| `code_name_map` | text | 待补 · 可空 |
| `type` | tinyint | 待补 |
| `status` | tinyint | 待补 |
| `error_msg` | text | 待补 · 可空 |
| `modify_time` | datetime | 待补 · 可空 |
| `id` | int | 待补 · 可空 |
| `config_id` | int | 待补 |
| `script` | text | 待补 · 可空 |
| `choose_field` | text | 待补 · 可空 |
| `code_name_map` | text | 待补 · 可空 |
| `type` | tinyint | 待补 |
| `status` | tinyint | 待补 |
| `error_msg` | text | 待补 · 可空 |
| `modify_time` | datetime | 待补 · 可空 |
| `Id` | int(11) | 自增Id · 可空 |
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
- `UK_AppId_DeletedAt`:AppId, DeletedAt (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
