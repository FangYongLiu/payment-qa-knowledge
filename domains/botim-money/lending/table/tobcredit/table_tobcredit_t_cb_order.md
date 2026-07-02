---
id: tbl_tobcredit_t_cb_order
object_type: Table
name: 订单表 (t_cb_order)
aliases: [t_cb_order, tobcredit.t_cb_order]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: tobcredit schema DDL
tags: [lending, tobcredit]
sensitivity: normal
related_services: []
---

# 订单表 (t_cb_order)

## 用途
物理表 `tobcredit.t_cb_order`,主键 `id`。订单表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主健 · 可空 |
| `amount` | decimal(19, 4) | 金额 |
| `partner_id` | varchar(20) | 商户ID |
| `status` | smallint(5) | 订单状态：0 待确认，1 已确认，-2 退款 |
| `bill_no` | varchar(64) | 帐单号 · 可空 |
| `refund_time` | timestamp | 退款时间 · 可空 |
| `refund_order_no` | varchar(32) | 退款订单号 · 可空 |
| `out_order_no` | varchar(32) | 外部订单号 · 可空 |
| `ext` | varchar(32) | 其它信息 · 可空 |
| `advant_partner_id` | varchar(20) | 垫资户 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`id`
- `idx_bill_no`:bill_no
- `idx_partner_id`:partner_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
