---
id: tbl_reconciliation_t_refund_order_flow
object_type: Table
name: 退款撤销订单 (t_refund_order_flow)
aliases: [t_refund_order_flow, reconciliation.t_refund_order_flow]
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: reconciliation schema DDL
tags: [settlement, reconciliation]
sensitivity: normal
related_services: []
---

# 退款撤销订单 (t_refund_order_flow)

## 用途
物理表 `reconciliation.t_refund_order_flow`,主键 `flow_id`。退款撤销订单。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `flow_id` | bigint(17) | 主键 |
| `fund_channel_code` | varchar(32) | 渠道编号 |
| `biz_type` | varchar(4) | 业务类型 |
| `inst_order_no` | varchar(64) | 机构订单号 |
| `amount` | decimal(15, 2) | 交易金额 · 可空 |
| `currency` | varchar(3) | 币种 · 可空 |
| `status` | varchar(4) | 状态 · 可空 |
| `payment_order_no` | varchar(64) | 支付订单号 · 可空 |
| `product_order_no` | varchar(64) | 产品订单号 · 可空 |
| `original_order_no` | varchar(64) | 原机构订单号 |
| `gmt_submit` | timestamp | 订单提交时间 · 可空 |
| `refund_type` | varchar(4) | 退款类型 · 可空 |
| `original_amount` | decimal(15, 2) | 原交易金额 · 可空 |
| `gmt_original` | timestamp | 原交易时间 · 可空 |
| `gmt_create` | timestamp | 创建时间 · 可空 |
| `gmt_modified` | timestamp | 更新时间 · 可空 |

## 主键 / 索引
- 主键:`flow_id`
- `uk_channel_biz_inst`:fund_channel_code, inst_order_no, biz_type (UNIQUE)
- `idx_original_order_no`:original_order_no

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
