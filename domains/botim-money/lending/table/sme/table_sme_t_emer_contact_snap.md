---
id: tbl_sme_t_emer_contact_snap
object_type: Table
name: Emergency contact snapshot information for the order (t_emer_contact_snap)
aliases: [t_emer_contact_snap, sme.t_emer_contact_snap]
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

# Emergency contact snapshot information for the order (t_emer_contact_snap)

## 用途
物理表 `sme.t_emer_contact_snap`,主键 `id`。Emergency contact snapshot information for the order。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 待补 · 可空 |
| `loan_order_no` | varchar(64) | order_no in table t_loan_order |
| `phone` | varchar(64) | Emergency contact number |
| `name` | varchar(64) | Emergency contact name |
| `relative` | varchar(32) | Emergency contact and borrower relationship |
| `create_time` | timestamp | 待补 · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
