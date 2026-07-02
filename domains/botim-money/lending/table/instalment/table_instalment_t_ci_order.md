---
id: tbl_instalment_t_ci_order
object_type: Table
name: 订单表 (t_ci_order)
aliases: [t_ci_order, instalment.t_ci_order]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: instalment schema DDL
tags: [lending, instalment]
sensitivity: normal
related_services: []
---

# 订单表 (t_ci_order)

## 用途
物理表 `instalment.t_ci_order`,主键 `id`。订单表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 主键 · 可空 |
| `status` | int | 状态 |
| `amount` | decimal(15, 2) | 订单金额 |
| `user_id` | varchar(50) | 用户ID |
| `credit_id` | int | 授信ID · 可空 |
| `vendor` | varchar(50) | 渠道 · 可空 |
| `period` | smallint | 借款期限 |
| `period_unit` | smallint | 期限单位：0 天 1 月 2年 |
| `finish_time` | timestamp | 支付完成时间 · 可空 |
| `rebate` | int | 利率 |
| `sku_id` | varchar(255) | 商品信息 · 可空 |
| `penalty` | int | 罚息利率 |
| `finish_repay_time` | timestamp | 实际还款时间 · 可空 |
| `order_no` | varchar(64) | 订单唯一ID |
| `is_read` | smallint | 状态已读未读 |
| `audit_start_time` | timestamp | 审核开始时间 · 可空 |
| `audit_finish_time` | timestamp | 审核结束时间 · 可空 |
| `product_code` | varchar(10) | 产品码 |
| `lenders` | varchar(20) | 资金方 |
| `fee` | decimal(15, 2) | 手续费 · 可空 |
| `ext` | varchar(255) | 扩展信息 · 可空 |
| `partner_id` | varchar(20) | 渠道 |
| `send_sku_status` | smallint(5) | 发货状态: 0 发货中 1 发货成功 -1 发货失败 · 可空 |
| `refund_status` | smallint(5) | 退款状态: 0 未退款  1 退款中 2退款成功 -2 退款失败 · 可空 |
| `send_sku_time` | timestamp | 发货时间 · 可空 |
| `refund_time` | timestamp | 退款时间 · 可空 |
| `sale_order_no` | varchar(64) | 关联销售订单号 · 可空 |
| `sale_partner_id` | varchar(32) | 商户ID · 可空 |
| `created_time` | timestamp | 创建时间 · 可空 |
| `last_modified` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_order_no`:order_no
- `idx_sale_order_no`:sale_order_no
- `idx_sale_partner_id`:sale_partner_id
- `idx_user_id`:user_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
