---
id: tbl_statement_t_statement_file
object_type: Table
name: 对账单文件 (t_statement_file)
aliases: [t_statement_file, statement.t_statement_file]
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

# 对账单文件 (t_statement_file)

## 用途
物理表 `statement.t_statement_file`,主键 `id`。对账单文件。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主键 · 可空 |
| `task_id` | bigint | 任务id |
| `period_id` | bigint | 账期id |
| `file_path` | varchar(500) | 文件路径 |
| `total_records` | int | 总记录数 |
| `created_time` | timestamp | 创建时间 |
| `merchant_mid` | varchar(32) | 商户ID · 可空 |
| `period_type` | varchar(32) | 期限类型 · 可空 |
| `begin_date` | timestamp | 开始时间 · 可空 |
| `end_date` | timestamp | 结束时间 · 可空 |
| `statement_type` | varchar(32) | 对账单类型 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_task_id`:task_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
