---
id: tbl_sme_t_lo_deal_event
object_type: Table
name: Loan order processing record form (t_lo_deal_event)
aliases: [t_lo_deal_event, sme.t_lo_deal_event]
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

# Loan order processing record form (t_lo_deal_event)

## 用途
物理表 `sme.t_lo_deal_event`,主键 `id`。Loan order processing record form。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 待补 · 可空 |
| `loan_order_no` | varchar(64) | order_no in table t_loan_order |
| `type` | tinyint | Event type |
| `create_time` | timestamp | Creation time |
| `memo` | varchar(64) | remark · 可空 |

## 主键 / 索引
- 主键:`id`
- `uk_id`:loan_order_no, type (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
