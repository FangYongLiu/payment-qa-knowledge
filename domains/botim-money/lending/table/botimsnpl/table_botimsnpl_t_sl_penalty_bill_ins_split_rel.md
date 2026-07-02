---
id: tbl_botimsnpl_t_sl_penalty_bill_ins_split_rel
object_type: Table
name: snpl penalty bill instalment split relation table (t_sl_penalty_bill_ins_split_rel)
aliases: [t_sl_penalty_bill_ins_split_rel, botimsnpl.t_sl_penalty_bill_ins_split_rel]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: botimsnpl schema DDL
tags: [lending, botimsnpl]
sensitivity: normal
related_services: []
---

# snpl penalty bill instalment split relation table (t_sl_penalty_bill_ins_split_rel)

## 用途
物理表 `botimsnpl.t_sl_penalty_bill_ins_split_rel`,主键 `id`。snpl penalty bill instalment split relation table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | primary key · 可空 |
| `penalty_bill_id` | int | penalty bill id |
| `ins_id` | int | instalment id |
| `status` | tinyint | 0 - valid, -1 - refund |
| `cope_penalty` | decimal(15, 2) | cope penalty amount |
| `already_repay_penalty` | decimal(15, 2) | already repay penalty amount |
| `ext` | varchar(255) | ext · 可空 |
| `created_time` | datetime | created time |
| `last_modified` | datetime | last modified time |

## 主键 / 索引
- 主键:`id`
- `idx_penalty_ins_ins_id`:ins_id
- `idx_penalty_ins_penalty_bill_id`:penalty_bill_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
