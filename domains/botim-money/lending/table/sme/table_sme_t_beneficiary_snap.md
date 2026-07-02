---
id: tbl_sme_t_beneficiary_snap
object_type: Table
name: Record the order account information (t_beneficiary_snap)
aliases: [t_beneficiary_snap, sme.t_beneficiary_snap]
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

# Record the order account information (t_beneficiary_snap)

## 用途
物理表 `sme.t_beneficiary_snap`,主键 `id`。Record the order account information。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 待补 · 可空 |
| `loan_order_no` | varchar(64) | order_no in table t_loan_order |
| `channel_type` | smallint | 待补 |
| `beneficiary_Identity_type` | varchar(32) | 待补 |
| `values` | can | 待补 · 可空 |
| `When` | channel | 待补 · 可空 |
| `values` | can | 待补 · 可空 |
| `beneficiary_identity` | varchar(32) | 待补 |
| `When` | beneficiary | 待补 · 可空 |
| `when` | beneficiary | 待补 · 可空 |
| `when` | beneficiary | 待补 · 可空 |
| `when` | channel | 待补 · 可空 |
| `When` | beneficiary | 待补 · 可空 |
| `When` | beneficiary | 待补 · 可空 |
| `beneficiary_full_name` | varchar(64) | Full name of payee |
| `beneficiary_address` | varchar(255) | 待补 · 可空 |
| `cannot` | be | 待补 · 可空 |
| `transfer_code` | varchar(64) | 待补 |
| `for` | beneficiary | 待补 |
| `for` | beneficiary | 待补 · 可空 |
| `create_time` | timestamp | 待补 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
