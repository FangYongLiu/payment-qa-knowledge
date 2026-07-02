---
id: tbl_rnpl_t_audit_record
object_type: Table
name: Risk Control Audit Record Table (t_audit_record)
aliases: [t_audit_record, rnpl.t_audit_record]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: rnpl schema DDL
tags: [lending, rnpl]
sensitivity: normal
related_services: []
---

# Risk Control Audit Record Table (t_audit_record)

## 用途
物理表 `rnpl.t_audit_record`,主键 `id`。Risk Control Audit Record Table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | id · 可空 |
| `application_id` | varchar(64) | applicationId passed to the wind control system (anubis) |
| `credit_order_id` | int | corresponds to the id field of the credit_order table. |
| `status` | smallint(4) | Status: 0: initial status, 1: under review, 2: review complete |
| `create_time` | timestamp | 待补 |
| `update_time` | timestamp | 待补 |
| `suggestion` | smallint(4) | 1:Audit Passed, 0: Audit Rejected · 可空 |
| `reason_code` | smallint(4) | Decision Reason Code: 200 :Pass, 500: Do not meet the conditions of the wind control refused, -1: audit timeout · 可空 |
| `amount` | decimal(10, 2) | amount approved · 可空 |
| `ext_info` | varchar(255) | json string, other data items returned by wind control, e.g. total_profit_rate · 可空 |

## 主键 / 索引
- 主键:`id`
- `uk_an`:application_id (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
