---
id: tbl_botimsnpl_t_sl_credit_snapshot
object_type: Table
name: 用户额度快照 (t_sl_credit_snapshot)
aliases: [t_sl_credit_snapshot, botimsnpl.t_sl_credit_snapshot]
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

# 用户额度快照 (t_sl_credit_snapshot)

## 用途
物理表 `botimsnpl.t_sl_credit_snapshot`,主键 `id`。用户额度快照。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 主键 · 可空 |
| `user_id` | varchar(20) | 用户ID |
| `order_no` | varchar(64) | 字段名 |
| `product_no` | varchar(32) | 产品 |
| `screen` | varchar(32) | 场景: REPAY OR CREATE_ORDER |
| `credit_amount` | decimal(15, 2) | 授信金额 |
| `temp_amount` | decimal(15, 2) | 临时金额 |
| `created_time` | timestamp | 创建日期 · 可空 |
| `last_modified` | timestamp | 修改日期 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_order_no`:order_no
- `idx_user_id`:user_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
