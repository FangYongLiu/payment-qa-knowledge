---
id: tbl_statement_t_statement_task
object_type: Table
name: 对账单任务 (t_statement_task)
aliases: [t_statement_task, statement.t_statement_task]
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

# 对账单任务 (t_statement_task)

## 用途
物理表 `statement.t_statement_task`,主键 `id`。对账单任务。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主键 · 可空 |
| `period_id` | bigint | 账期id |
| `registration_id` | bigint | 登记id |
| `status` | varchar(32) | 状态 CREATED 已创建；GERATED 已生成；UPLOADED 已上传；FINISHED 已完成 |
| `error_code` | varchar(50) | 错误码 · 可空 |
| `error_message` | varchar(500) | 错误信息 · 可空 |
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
