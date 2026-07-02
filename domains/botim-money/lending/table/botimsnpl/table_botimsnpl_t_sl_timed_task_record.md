---
id: tbl_botimsnpl_t_sl_timed_task_record
object_type: Table
name: 需要记录的定时任务执行记录表 (t_sl_timed_task_record)
aliases: [t_sl_timed_task_record, botimsnpl.t_sl_timed_task_record]
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

# 需要记录的定时任务执行记录表 (t_sl_timed_task_record)

## 用途
物理表 `botimsnpl.t_sl_timed_task_record`,主键 `id`。需要记录的定时任务执行记录表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 待补 · 可空 |
| `task_name` | varchar(64) | 待补 |
| `type` | smallint | 1、账单开duedate发票的任务 |
| `status` | smallint | 待补 |
| `create_time` | timestamp | 待补 |
| `update_time` | timestamp | 待补 |

## 主键 / 索引
- 主键:`id`
- `uk_tn`:task_name, type (UNIQUE)
- `ix_time`:create_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
