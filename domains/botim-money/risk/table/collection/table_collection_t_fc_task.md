---
id: tbl_collection_t_fc_task
object_type: Table
name: 任务表 (t_fc_task)
aliases: [t_fc_task, collection.t_fc_task]
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: collection schema DDL
tags: [risk, collection]
sensitivity: normal
related_services: []
---

# 任务表 (t_fc_task)

## 用途
物理表 `collection.t_fc_task`,主键 `id`。任务表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(10) | 主健 · 可空 |
| `create_by` | varchar(50) | 创建者 · 可空 |
| `update_by` | varchar(50) | 更新人员 · 可空 |
| `create_time` | timestamp | 创建时间 · 可空 |
| `update_time` | timestamp | 更新时间 · 可空 |
| `uid` | varchar(20) | id |
| `date` | date | 日期 |
| `name` | varchar(10) | 任务名 |
| `start_time` | timestamp | 开始时间 · 可空 |
| `end_time` | timestamp | 结束时间 · 可空 |
| `cost_time` | int(5) | 用时 |
| `total_round` | tinyint(5) | 总轮次 |
| `status` | tinyint(5) | 状态 初始0 进行中1 结束2 暂停-1 |

## 主键 / 索引
- 主键:`id`
- `idx_date`:date
- `idx_uid`:uid

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
