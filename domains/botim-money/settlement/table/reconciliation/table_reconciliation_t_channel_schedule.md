---
id: tbl_reconciliation_t_channel_schedule
object_type: Table
name: 渠道任务计划 (t_channel_schedule)
aliases: [t_channel_schedule, reconciliation.t_channel_schedule]
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

# 渠道任务计划 (t_channel_schedule)

## 用途
物理表 `reconciliation.t_channel_schedule`,主键 `flow_id`。渠道任务计划。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `flow_id` | bigint(17) | 主键 |
| `task_type` | varchar(8) | 任务类型 · 可空 |
| `fund_channel_code` | varchar(32) | 渠道编号 · 可空 |
| `biz_type` | varchar(4) | 业务类型 · 可空 |
| `status` | varchar(4) | 状态  Y启用 N 不启用 · 可空 |
| `last_exec_time` | timestamp | 上次执行时间 · 可空 |
| `next_exec_time` | timestamp | 下次执行时间 · 可空 |
| `trigger_cron` | varchar(32) | 触发cron · 可空 |
| `weight` | tinyint | 权重 · 可空 |
| `lock_tag` | varchar(4) | 锁状态 · 可空 |
| `notify_type` | varchar(128) | 通知类型 · 可空 |
| `notify_address` | varchar(255) | 通知地址 · 可空 |
| `memo` | varchar(255) | 备注 · 可空 |
| `operator` | varchar(64) | 操作者 · 可空 |
| `gmt_create` | timestamp | 创建时间 · 可空 |
| `gmt_modified` | timestamp | 更新时间 · 可空 |

## 主键 / 索引
- 主键:`flow_id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
