---
id: tbl_basiscustomer_t_audit_log
object_type: Table
name: 审核日志 (t_audit_log)
aliases: [t_audit_log, basiscustomer.t_audit_log]
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: basiscustomer schema DDL
tags: [activation, basiscustomer]
sensitivity: normal
related_services: []
---

# 审核日志 (t_audit_log)

## 用途
物理表 `basiscustomer.t_audit_log`,主键 `log_id`。审核日志。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `log_id` | bigint | 日志ID：前八后九 |
| `audit_id` | bigint | 审核ID |
| `operator` | varchar(32) | 操作人 |
| `action` | char | 操作：P通过，D拒绝，R重试 |
| `remark` | varchar(255) | 评论 · 可空 |
| `extension` | varchar(255) | 扩展字段 · 可空 |
| `create_time` | timestamp | 操作时间 |

## 主键 / 索引
- 主键:`log_id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
