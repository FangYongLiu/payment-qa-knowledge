---
id: tbl_botimsnpl_t_sl_push_config
object_type: Table
name: Scheduled push configuration table (t_sl_push_config)
aliases: [t_sl_push_config, botimsnpl.t_sl_push_config]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: botimsnpl schema DDL
tags: [lending, botimsnpl]
sensitivity: normal
related_services: []
---

# Scheduled push configuration table (t_sl_push_config)

## 用途
物理表 `botimsnpl.t_sl_push_config`,主键 `id`。Scheduled push configuration table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | Primary key · 可空 |
| `created_time` | timestamp | Creation time · 可空 |
| `last_modified` | timestamp | Last modified time · 可空 |
| `start` | int(5) | Start of overdue days · 可空 |
| `end` | int(5) | End of overdue days · 可空 |
| `msg_content` | varchar(500) | SMS message content · 可空 |
| `time` | varchar(100) | Execution time |
| `target` | int(5) | Target: 0 for botim, 1 for SMS |
| `param` | varchar(255) | Placeholder replacement parameters for the message · 可空 |
| `status` | int(5) | 0: Inactive; 1: Active |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
