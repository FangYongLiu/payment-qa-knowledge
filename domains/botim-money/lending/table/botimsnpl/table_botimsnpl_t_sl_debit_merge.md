---
id: tbl_botimsnpl_t_sl_debit_merge
object_type: Table
name: merge debit table (t_sl_debit_merge)
aliases: [t_sl_debit_merge, botimsnpl.t_sl_debit_merge]
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

# merge debit table (t_sl_debit_merge)

## 用途
物理表 `botimsnpl.t_sl_debit_merge`,主键 `id`。merge debit table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 待补 · 可空 |
| `created_time` | timestamp | created_time · 可空 |
| `user_id` | varchar(20) | user id |
| `request_no` | varchar(64) | request no |
| `status` | tinyint(5) | status |
| `ext` | varchar(256) | ext · 可空 |
| `amount` | decimal(10, 2) | amount · 可空 |
| `unrepay_capital` | decimal(10, 2) | unrepay_capital · 可空 |
| `updated_time` | timestamp | 待补 |

## 主键 / 索引
- 主键:`id`
- `idx_request_no`:request_no
- `idx_user_id`:user_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
