---
id: tbl_botimsnpl_t_sl_ins_split
object_type: Table
name: 还款分帐 (t_sl_ins_split)
aliases: [t_sl_ins_split, botimsnpl.t_sl_ins_split]
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

# 还款分帐 (t_sl_ins_split)

## 用途
物理表 `botimsnpl.t_sl_ins_split`,主键 `id`。还款分帐。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int unsigned | 主键 · 可空 |
| `record_id` | int | 记录表 |
| `ins_id` | int | 帐单表 |
| `ins_repay_capital` | decimal(15, 2) | 本金 |
| `ins_repay_penalty` | decimal(15, 2) | 罚息 · 可空 |
| `ins_repay_fee` | decimal(15, 2) | 费用 · 可空 |
| `created_time` | timestamp | 创建时间 · 可空 |
| `last_modified` | timestamp | 更新时间 · 可空 |
| `ext` | varchar(255) | ext · 可空 |
| `early_settlement_fee` | decimal(15, 2) | early settlement fee · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_ins_id`:ins_id
- `idx_record_id`:record_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
