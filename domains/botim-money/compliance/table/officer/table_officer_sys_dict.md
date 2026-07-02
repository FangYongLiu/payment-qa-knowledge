---
id: tbl_officer_sys_dict
object_type: Table
name: Data dictionary (sys_dict)
aliases: [sys_dict, officer.sys_dict]
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

# Data dictionary (sys_dict)

## 用途
物理表 `officer.sys_dict`,主键 `dict_id`。Data dictionary。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `dict_id` | bigint | ID · 可空 |
| `name` | varchar(255) | Dictionary name |
| `description` | varchar(255) | Description · 可空 |
| `create_by` | varchar(255) | creator · 可空 |
| `update_by` | varchar(255) | Updater · 可空 |
| `create_time` | timestamp | Creation date · 可空 |
| `update_time` | timestamp | Update time · 可空 |

## 主键 / 索引
- 主键:`dict_id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
