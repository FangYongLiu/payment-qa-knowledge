---
id: tbl_botimsnpl_t_sl_fee_changelog
object_type: Table
name: 费用记录表 (t_sl_fee_changelog)
aliases: [t_sl_fee_changelog, botimsnpl.t_sl_fee_changelog]
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

# 费用记录表 (t_sl_fee_changelog)

## 用途
物理表 `botimsnpl.t_sl_fee_changelog`,主键 `id`。费用记录表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int unsigned | 主键 · 可空 |
| `bill_id` | int | 记录表 · 可空 |
| `ins_id` | int | 帐单表 · 可空 |
| `user_id` | varchar(20) | 用户ID |
| `after_fee` | decimal(15, 2) | 更新后金额 |
| `before_fee` | decimal(15, 2) | 更新前 · 可空 |
| `amount` | decimal(15, 2) | 金额 · 可空 |
| `type` | smallint | 类型: 0 帐单 1 instalment |
| `created_time` | timestamp | 创建时间 · 可空 |
| `last_modified` | timestamp | 更新时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_bill_id`:bill_id
- `idx_ins_id`:ins_id
- `idx_user_id`:user_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
