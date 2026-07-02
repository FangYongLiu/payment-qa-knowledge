---
id: tbl_sme_t_repay_split_user
object_type: Table
name: Payment sharing account (t_repay_split_user)
aliases: [t_repay_split_user, sme.t_repay_split_user]
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

# Payment sharing account (t_repay_split_user)

## 用途
物理表 `sme.t_repay_split_user`,主键 `id`。Payment sharing account。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int(11) | 待补 · 可空 |
| `loan_order_no` | varchar(50) | Order number |
| `repay_record_id` | int | t_repay_record |
| `bill_id` | int | bill · 可空 |
| `repay_capital` | decimal(15, 2) | principal · 可空 |
| `repay_interest` | decimal(15, 2) | interest · 可空 |
| `repay_penalty` | decimal(15, 2) | Interest penalty · 可空 |
| `early_settlement_fee` | decimal(15, 2) | Settle charges early · 可空 |
| `currency` | char(3) | 待补 |
| `create_time` | timestamp | Creation time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
