---
id: tbl_reconciliation_t_channel_task
object_type: Table
name: 渠道任务记录 (t_channel_task)
aliases: [t_channel_task, reconciliation.t_channel_task]
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: reconciliation schema DDL
tags: [settlement, reconciliation]
sensitivity: normal
related_services: []
---

# 渠道任务记录 (t_channel_task)

## 用途
物理表 `reconciliation.t_channel_task`,主键 `flow_id`。渠道任务记录。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `flow_id` | bigint(17) | 主键 |
| `task_type` | varchar(4) | 任务类型 · 可空 |
| `fund_channel_code` | varchar(64) | 渠道编号 · 可空 |
| `biz_type` | varchar(4) | 业务类型 · 可空 |
| `start_date` | date | 起始日期 · 可空 |
| `end_date` | date | 截止日期 · 可空 |
| `status` | varchar(8) | 任务状态 · 可空 |
| `origin_flow` | varchar(64) | 关联流水号 · 可空 |
| `message` | varchar(255) | 任务执行信息 · 可空 |
| `notify_status` | varchar(8) | 通知状态 · 可空 |
| `notify_message` | varchar(255) | 通知描述信息 · 可空 |
| `gmt_create` | timestamp | 创建时间 · 可空 |
| `gmt_modified` | timestamp | 更新时间 · 可空 |
| `plan_time` | timestamp | 任务计划执行时间 · 可空 |
| `exec_time` | timestamp | 任务实际执行时间 · 可空 |

## 主键 / 索引
- 主键:`flow_id`
- `idx_date`:start_date, end_date

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
