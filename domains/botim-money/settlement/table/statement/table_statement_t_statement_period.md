---
id: tbl_statement_t_statement_period
object_type: Table
name: 账期 (t_statement_period)
aliases: [t_statement_period, statement.t_statement_period]
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: statement schema DDL
tags: [settlement, statement]
sensitivity: normal
related_services: []
---

# 账期 (t_statement_period)

## 用途
物理表 `statement.t_statement_period`,主键 `id`。账期。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主键 · 可空 |
| `template_id` | bigint | 模板id |
| `status` | varchar(50) | 状态 CREATED 已创建;  STARTED 已开始；DISPATCHED 已匹配；FINISHED 已完成 |
| `total_task_nums` | int | 总任务数 |
| `completed_task_nums` | int | 已完成任务数 |
| `begin_date` | timestamp | 开始日期 |
| `end_date` | timestamp | 结束日期 |
| `created_time` | timestamp | 创建时间 |
| `last_updated_time` | timestamp | 最后更新时间 |
| `data_version` | bigint | 数据版本 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
