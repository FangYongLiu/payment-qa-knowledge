---
id: tbl_rnpl_t_pay_record_rp_split
object_type: Table
name: bill and repay record split (t_pay_record_rp_split)
aliases: [t_pay_record_rp_split, rnpl.t_pay_record_rp_split]
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

# bill and repay record split (t_pay_record_rp_split)

## 用途
物理表 `rnpl.t_pay_record_rp_split`,主键 `id`。bill and repay record split。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int unsigned | id · 可空 |
| `loan_order_id` | int | loan order id |
| `loan_order_no` | varchar(64) | loan order No |
| `pay_record_rp_id` | int | repay pay record id |
| `bill_id` | int | bill id |
| `repay_principal` | decimal(15, 2) | principal |
| `repay_instalment_fee` | decimal(15, 2) | instalment fee |
| `repay_penalty` | decimal(15, 2) | penalty |
| `create_time` | timestamp | create time |
| `update_time` | timestamp | update time |
| `currency` | char(3) | currency |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
