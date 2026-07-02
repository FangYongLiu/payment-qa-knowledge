---
id: tbl_botimcredit_t_cb_collection_message_config
object_type: Table
name: Collection payment reminder message configuration (t_cb_collection_message_config)
aliases: [t_cb_collection_message_config, botimcredit.t_cb_collection_message_config]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: botimcredit schema DDL
tags: [lending, botimcredit]
sensitivity: normal
related_services: []
---

# Collection payment reminder message configuration (t_cb_collection_message_config)

## 用途
物理表 `botimcredit.t_cb_collection_message_config`,主键 `id`。Collection payment reminder message configuration。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | Primary key · 可空 |
| `message_type` | varchar(50) | Message type: SINGLE_BILL, OVERDUE_BILL |
| `days_offset` | int | Days before/after due date (negative for before, positive for after) |
| `execution_hour` | int | Execution time (hour of day, 0-23) |
| `message_title` | varchar(200) | Message title |
| `message_content` | text | Message content template (supports placeholders: #amount, #dueDate, #month, #overdueDay) |
| `cta_text` | varchar(100) | Call to action text · 可空 |
| `landing_page` | varchar(500) | Landing page URL · 可空 |
| `target_channel` | int | Target channel: 0=TOTOK, 1=SMS, 2=BOTH |
| `status` | int | Status: 0=INACTIVE, 1=ACTIVE |
| `created_time` | timestamp | Created time |
| `last_modified` | timestamp | Last modified time |
| `created_by` | varchar(50) | Created by · 可空 |
| `last_modified_by` | varchar(50) | Last modified by · 可空 |
| `description` | varchar(500) | Description for admin reference · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
