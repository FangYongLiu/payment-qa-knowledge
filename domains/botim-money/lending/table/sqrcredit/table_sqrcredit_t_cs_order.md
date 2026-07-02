---
id: tbl_sqrcredit_t_cs_order
object_type: Table
name: 交易订单表 (t_cs_order)
aliases: [t_cs_order, sqrcredit.t_cs_order]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: sqrcredit schema DDL
tags: [lending, sqrcredit]
sensitivity: normal
related_services: []
---

# 交易订单表 (t_cs_order)

## 用途
物理表 `sqrcredit.t_cs_order`,主键 `id`。交易订单表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 主键 · 可空 |
| `status` | smallint(5) | paylater 订单状态 |
| `amount` | decimal(15, 2) | 金额 |
| `user_id` | varchar(50) | 用户ID |
| `product_desc` | varchar(50) | 商品描述 |
| `due_time` | timestamp | 还款日 · 可空 |
| `bill_no` | varchar(64) | ID |
| `origin_order_no` | varchar(64) | 退款原始订单号 · 可空 |
| `out_order_no` | varchar(64) | 外部订单号 |
| `created_time` | timestamp | 创建时间 · 可空 |
| `last_modified` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_bill_no`:bill_no
- `idx_out_order_no`:out_order_no
- `idx_user_id`:user_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
