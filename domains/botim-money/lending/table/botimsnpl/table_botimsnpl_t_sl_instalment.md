---
id: tbl_botimsnpl_t_sl_instalment
object_type: Table
name: 帐单表 (t_sl_instalment)
aliases: [t_sl_instalment, botimsnpl.t_sl_instalment]
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

# 帐单表 (t_sl_instalment)

## 用途
物理表 `botimsnpl.t_sl_instalment`,主键 `id`。帐单表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 主键 · 可空 |
| `status` | int | 状态: 0 待还款 1  结清 |
| `amount` | decimal(15, 2) | 金额 |
| `periods` | int | 期数 |
| `overdue_days` | int(5) | 逾期天数 |
| `check_time` | timestamp | 出帐日期 · 可空 |
| `due_time` | timestamp | 还款日期 · 可空 |
| `check_amount` | decimal(15, 2) | 出帐金额 · 可空 |
| `finish_repay_time` | timestamp | 完结日期 · 可空 |
| `early_settlement_fee` | decimal(15, 2) | early settlement fee · 可空 |
| `unearned_interest` | decimal(15, 2) | unearned interest · 可空 |
| `user_id` | varchar(20) | 用户ID |
| `cope_capital` | decimal(15, 2) | 应还本金 |
| `cope_fee` | decimal(15, 2) | 应还利息 |
| `cope_penalty` | decimal(15, 2) | 应还罚息 |
| `already_repay_capital` | decimal(15, 2) | 已还本金 |
| `already_repay_fee` | decimal(15, 2) | 已还利息 |
| `already_repay_penalty` | decimal(15, 2) | 已还罚息 |
| `reverse_way` | varchar(10) | 冲帐方式 · 可空 |
| `monthly` | varchar(20) | 月份 · 可空 |
| `order_no` | varchar(64) | 订单ID |
| `created_time` | timestamp | 创建日期 · 可空 |
| `last_modified` | timestamp | 修改日期 · 可空 |
| `ext` | varchar(255) | ext · 可空 |
| `is_extended` | smallint | Extension flag: 0=No, 1=Yes · 可空 |
| `original_due_time` | timestamp | Original due date (before extension) · 可空 |
| `cope_extension_fee` | decimal(15, 2) | Extension fee share (incl. VAT) · 可空 |
| `already_extension_fee` | decimal(15, 2) | Extension fee collected · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_monthly`:monthly
- `idx_order_no`:order_no
- `idx_user_id`:user_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
