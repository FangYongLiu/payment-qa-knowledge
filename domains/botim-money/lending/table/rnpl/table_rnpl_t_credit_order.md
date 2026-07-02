---
id: tbl_rnpl_t_credit_order
object_type: Table
name: Advance Credit Application Table (t_credit_order)
aliases: [t_credit_order, rnpl.t_credit_order]
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

# Advance Credit Application Table (t_credit_order)

## 用途
物理表 `rnpl.t_credit_order`,主键 `id`。Advance Credit Application Table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | primary Key · 可空 |
| `order_no` | varchar(64) | unique id for credit application order |
| `user_id` | varchar(20) | user id |
| `product_code` | char(4) | product code: fixed value for RNPL |
| `status` | smallint(4) | Status, 1: Audit in progress, -2 Audit rejected, 2: Audit passed |
| `audit_start_time` | timestamp | submission Review Time · 可空 |
| `audit_finish_time` | timestamp | audit End Time · 可空 |
| `result_audit_record_id` | int | review records that give the final credit result · 可空 |
| `audit_info` | varchar(512) | json string to record the audit information carried by a single credit audit, where the audit information refers only to the information filled in by the user in the application process. rnpl the information carried includes the contents of the t_user_rental_intention table · 可空 |
| `create_time` | timestamp | create time |
| `update_time` | timestamp | update time |

## 主键 / 索引
- 主键:`id`
- `uk_on`:order_no (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
