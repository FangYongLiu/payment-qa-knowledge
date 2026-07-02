---
id: tbl_officer_sys_role
object_type: Table
name: role table (sys_role)
aliases: [sys_role, officer.sys_role]
domain: compliance
status: active
owner: dewen.li
reviewer: dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: officer schema DDL
tags: [compliance, officer]
sensitivity: normal
related_services: []
---

# role table (sys_role)

## 用途
物理表 `officer.sys_role`,主键 `role_id`。role table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `role_id` | bigint | ID · 可空 |
| `name` | varchar(255) | Name |
| `level` | int | Role level · 可空 |
| `description` | varchar(100) | Description · 可空 |
| `data_scope` | varchar(100) | Data permissions · 可空 |
| `create_by` | varchar(100) | creator · 可空 |
| `update_by` | varchar(100) | Updater · 可空 |
| `create_time` | timestamp | Creation date · 可空 |
| `update_time` | timestamp | Update time · 可空 |

## 主键 / 索引
- 主键:`role_id`
- `uk_uniq_name`:name (UNIQUE)
- `idx_role`:name

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
