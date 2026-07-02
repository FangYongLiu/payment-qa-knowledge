---
id: tbl_sme_t_audit_record
object_type: Table
name: Risk control audit record form (t_audit_record)
aliases: [t_audit_record, sme.t_audit_record]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: sme schema DDL
tags: [lending, sme]
sensitivity: normal
related_services: []
---

# Risk control audit record form (t_audit_record)

## 用途
物理表 `sme.t_audit_record`,主键 `id`。Risk control audit record form。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 待补 · 可空 |
| `loan_order_no` | varchar(64) | order_no in table t_loan_order |
| `application_id` | varchar(64) | Credit application order unique ID |
| `status` | smallint | Status, 0: not submitted, 1: under review, -2 Rejected, 2: approved |
| `audit_start_time` | timestamp | Submission time · 可空 |
| `audit_finish_time` | timestamp | Audit closing time · 可空 |
| `refuse_reason` | varchar(255) | Review reasons for rejection at the time of rejection · 可空 |
| `create_time` | timestamp | Creation time |
| `update_time` | timestamp | Modification time |

## 主键 / 索引
- 主键:`id`
- `uk_on`:application_id (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
