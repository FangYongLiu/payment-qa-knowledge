---
id: tbl_collection_t_col_order_info
object_type: Table
name: 关联订单信息 (t_col_order_info)
aliases: [t_col_order_info, collection.t_col_order_info]
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: collection schema DDL
tags: [risk, collection]
sensitivity: normal
related_services: []
---

# 关联订单信息 (t_col_order_info)

## 用途
物理表 `collection.t_col_order_info`,主键 `id`。关联订单信息。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主健 · 可空 |
| `create_by` | varchar(100) | 创建者 · 可空 |
| `create_time` | timestamp | 创建时间 · 可空 |
| `update_time` | timestamp | 更新时间 · 可空 |
| `update_by` | varchar(100) | 更新人员 · 可空 |
| `member_id` | varchar(32) | 会员ID |
| `order_no` | varchar(64) | 订单 |
| `total_amount` | decimal(15, 2) | 总金额 · 可空 |
| `downpayment_amount` | decimal(15, 2) | 首付金额 · 可空 |
| `instalment_amount` | decimal(15, 2) | 分期金额 · 可空 |
| `merchant_partner_id` | varchar(64) | 商户id |
| `merchant_name` | varchar(64) | 商户名称 · 可空 |
| `type` | smallint(11) | 业务类型 1手机分期 |
| `brand` | varchar(64) | 品牌 · 可空 |
| `model` | varchar(64) | 型号 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_member_id`:member_id
- `idx_merchant_partner_id`:merchant_partner_id
- `idx_order`:order_no

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
