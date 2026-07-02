---
id: tbl_credit_t_cs_card_limit
object_type: Table
name: 用户提额限制表 (t_cs_card_limit)
aliases: [t_cs_card_limit, credit.t_cs_card_limit]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: credit schema DDL
tags: [lending, credit]
sensitivity: normal
related_services: []
---

# 用户提额限制表 (t_cs_card_limit)

## 用途
物理表 `credit.t_cs_card_limit`,主键 `id`。用户提额限制表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 待补 · 可空 |
| `created_time` | timestamp | 创建时间 · 可空 |
| `user_id` | varchar(20) | 用户ID |
| `order_no` | varchar(64) | 查询时订单号 |
| `is_limit` | tinyint(5) | 是否限额 |
| `limit14d` | decimal(10, 2) | 14天限额 · 可空 |
| `limit28d` | decimal(10, 2) | 28天限额 · 可空 |
| `limit2m` | decimal(10, 2) | 2期限额 · 可空 |
| `limit3m` | decimal(10, 2) | 3期限额 · 可空 |
| `limit6m` | decimal(10, 2) | 6期限额 · 可空 |
| `risk_level_json` | varchar(50) | risk level json · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_order_no`:order_no
- `idx_user_id`:user_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
