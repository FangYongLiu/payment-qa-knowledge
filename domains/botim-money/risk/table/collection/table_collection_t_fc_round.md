---
id: tbl_collection_t_fc_round
object_type: Table
name: 任务轮次表 (t_fc_round)
aliases: [t_fc_round, collection.t_fc_round]
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

# 任务轮次表 (t_fc_round)

## 用途
物理表 `collection.t_fc_round`,主键 `id`。任务轮次表。业务语义细节**待补**(表结构来自 DDL)。

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
| `task_uid` | varchar(20) | 任务id |
| `uid` | varchar(40) | id |
| `date` | date | 日期 |
| `name` | varchar(20) | 轮次内容 |
| `start_time` | timestamp | 开始时间 · 可空 |
| `end_time` | timestamp | 结束时间 · 可空 |
| `cost_time` | int(5) | 花费时间 |
| `current_round` | tinyint(5) | 当前轮次 |
| `status` | tinyint(5) | 初始0 进行中1 结束2 暂停-1 |
| `type` | tinyint(5) | 1基础 2额外 |
| `count` | int(5) | 总数 |
| `finish_count` | int(5) | 完成数 |
| `ptp_count` | int(5) | ptp数 |
| `user_count` | int(5) | 用户数 |
| `repay_count` | int(5) | 还款数 |

## 主键 / 索引
- 主键:`id`
- `idx_date`:date
- `idx_task_uid`:task_uid
- `idx_uid`:uid

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
