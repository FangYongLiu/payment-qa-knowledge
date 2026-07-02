---
id: tbl_sqrcredit_t_cs_setted_order
object_type: Table
name: 结算订单 (t_cs_setted_order)
aliases: [t_cs_setted_order, sqrcredit.t_cs_setted_order]
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

# 结算订单 (t_cs_setted_order)

## 用途
物理表 `sqrcredit.t_cs_setted_order`,主键 `id`。结算订单。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int(11) | 待补 · 可空 |
| `order_no` | varchar(64) | 订单ID |
| `amount` | decimal(15, 2) | 还款金额 |
| `status` | varchar(20) | 状态 |
| `created_time` | timestamp | 创建时间 · 可空 |
| `last_modified` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_order_no`:order_no

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
