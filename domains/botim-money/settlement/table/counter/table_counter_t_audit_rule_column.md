---
id: tbl_counter_t_audit_rule_column
object_type: Table
name: Column of Audit Application Rule (t_audit_rule_column)
aliases: [t_audit_rule_column, counter.t_audit_rule_column]
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: counter schema DDL
tags: [settlement, counter]
sensitivity: normal
related_services: []
---

# Column of Audit Application Rule (t_audit_rule_column)

## 用途
物理表 `counter.t_audit_rule_column`,主键 `column_id`。Column of Audit Application Rule。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `column_id` | bigint | Column ID |
| `audit_type` | varchar(16) | Audit Type |
| `column_name` | varchar(100) | Column Name |
| `display_name_cn` | varchar(100) | Dislay Name in Chinese |
| `display_name_en` | varchar(100) | Dislay Name in English |
| `data_type` | varchar(50) | Data Type：STRING，NUMBER · 可空 |
| `create_by` | bigint | Create User · 可空 |
| `create_time` | timestamp | Create Time · 可空 |
| `update_by` | bigint | Update User · 可空 |
| `update_time` | timestamp | Update Time · 可空 |

## 主键 / 索引
- 主键:`column_id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
