---
id: tbl_aml_t_cs_appeal
object_type: Table
name: CS Appeal Table (t_cs_appeal)
aliases: [t_cs_appeal, aml.t_cs_appeal]
domain: compliance
status: active
owner: dewen.li
reviewer: dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: aml schema DDL
tags: [compliance, aml]
sensitivity: normal
related_services: []
---

# CS Appeal Table (t_cs_appeal)

## 用途
物理表 `aml.t_cs_appeal`,主键 `id`。CS Appeal Table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key · 可空 |
| `apply_id` | varchar(32) | Appeal ID |
| `payment_order_no` | varchar(64) | Payment order number · 可空 |
| `transaction_id` | varchar(64) | Transaction ID · 可空 |
| `member_id` | varchar(20) | Member ID |
| `operator` | varchar(64) | Operator (CS agent) |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`id`
- `uk_apply_id`:apply_id (UNIQUE)
- `idx_member_id`:member_id
- `idx_payment_order_no`:payment_order_no
- `idx_update_time`:update_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
