---
id: tbl_instalment_t_ci_sale_order
object_type: Table
name: 电商订单 (t_ci_sale_order)
aliases: [t_ci_sale_order, instalment.t_ci_sale_order]
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

# 电商订单 (t_ci_sale_order)

## 用途
物理表 `instalment.t_ci_sale_order`,主键 `id`。电商订单。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int(11) | 主健 · 可空 |
| `status` | smallint(5) | 订单状态 |
| `sku_id` | int | 商品ID |
| `pay_mid` | varchar(64) | 付款方用户ID · 可空 |
| `sale_price` | decimal(10, 2) | 销售价格 |
| `count` | smallint | 数量 |
| `creator_role` | varchar(64) | 订单创建者角色 · 可空 |
| `creator_mid` | varchar(64) | 订单创建者 · 可空 |
| `global_no` | varchar(64) | 全局ID · 可空 |
| `qr_url` | varchar(255) | 订单二维码 · 可空 |
| `period_unit` | smallint(5) | 期数单位 |
| `period` | smallint (2) | 期数 |
| `order_no` | varchar(32) | 订单号 |
| `purchase_price` | decimal(10, 2) | 购买价格 |
| `user_note` | varchar(255) | 用户备注 · 可空 |
| `sys_note` | varchar(255) | 系统备注 · 可空 |
| `created_time` | timestamp | 创建时间 |
| `updated_time` | timestamp | 更新时间 |
| `credit_order_no` | varchar(64) | 信贷订单 · 可空 |
| `settle_time` | timestamp | 结算时间 · 可空 |
| `is_settled` | smallint(2) | 是否结算 |
| `partner_id` | varchar(32) | 商户ID |
| `deliver_photo` | varchar(100) | 发货验证照片 · 可空 |
| `ins_order_no` | varchar(64) | 渠道订单号 · 可空 |
| `is_refund` | smallint(2) | 是否退款 |
| `refund_time` | timestamp | 退款时间 · 可空 |
| `fee_rate` | double(4, 2) | 用户选择费率 · 可空 |
| `store_name` | varchar(200) | 商户名称 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_credit_no`:credit_order_no
- `idx_global_no`:global_no
- `idx_order_no`:order_no
- `idx_pay_mid`:pay_mid

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
