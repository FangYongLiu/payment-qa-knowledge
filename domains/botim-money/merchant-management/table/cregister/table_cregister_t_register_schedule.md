---
id: tbl_cregister_t_register_schedule
object_type: Table
name: Registration Schedule (t_register_schedule)
aliases: [t_register_schedule, cregister.t_register_schedule]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: cregister schema DDL
tags: [merchant-management, cregister]
sensitivity: normal
related_services: []
---

# Registration Schedule (t_register_schedule)

## 用途
物理表 `cregister.t_register_schedule`,主键 `id`。Registration Schedule。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | Primary Key ID · 可空 |
| `fund_provider_code` | varchar(24) | Channel Provider |
| `inst_code` | varchar(24) | Institution Code |
| `fund_channel_code` | varchar(24) | Channel Code |
| `task_type` | varchar(12) | Task Type; SR: Submit Registration, RA: Receipt Analysis |
| `processor` | varchar(15) | Processor Type · 可空 |
| `cron` | varchar(125) | Expression; Used to calculate the next execution time |
| `last_trigger_time` | timestamp | Last Trigger Time; Updated to this when each execution occurs |
| `next_trigger_time` | timestamp | Next Trigger Time; Calculated based on cron each time |
| `delay_time` | int | Delayed Execution Time; In minutes, delays next_trigger_time by this amount · 可空 |
| `is_locked` | char | Is Locked, Y/N |
| `status` | char | Status; N: Inactive, Y: Active |
| `gmt_create` | timestamp | Creation Time |
| `gmt_modified` | timestamp | Update Time |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
