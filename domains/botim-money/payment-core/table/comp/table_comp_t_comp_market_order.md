---
id: tbl_comp_t_comp_market_order
object_type: Table
name: 营销补偿 (t_comp_market_order)
aliases: [t_comp_market_order, comp.t_comp_market_order]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: comp schema DDL
tags: [payment-core, comp]
sensitivity: normal
related_services: []
---

# 营销补偿 (t_comp_market_order)

## 用途
物理表 `comp.t_comp_market_order`,主键 `order_no`。营销补偿。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `order_no` | bigint | 主键id |
| `comp_identity` | varchar(255) | 补偿标识 |
| `comp_activity_id` | varchar(64) | 关联补偿活动 |
| `tool_id` | int | 补偿工具id |
| `coupon_entity_id` | bigint | 补偿实体id · 可空 |
| `pay_member_id` | varchar(32) | 补偿付款方 |
| `to_member_id` | varchar(32) | 被补偿对象 |
| `account_type` | varchar(16) | 被补偿对象账户类型 现金类必须 |
| `type` | varchar(16) | 营销补偿类型 cash，coupon |
| `discount` | decimal(8, 4) | 折扣比例 · 可空 |
| `discount_limit` | decimal(8, 4) | 折扣金额上限 · 可空 |
| `effective_time` | timestamp | 生效时间 |
| `expiry_time` | timestamp | 失效时间 |
| `use_threshold` | decimal(15, 4) | 使用门槛 |
| `amount` | decimal(15, 4) | 补偿额度 · 可空 |
| `currency` | char(3) | 币种 |
| `status` | varchar(16) | 状态 |
| `extension` | varchar(128) | 扩展字段 · 可空 |
| `memo` | varchar(128) | 备注 · 可空 |
| `error_code` | varchar(32) | 错误code · 可空 |
| `error_msg` | varchar(128) | 错误描述 · 可空 |
| `created_time` | timestamp | 创建时间 |
| `updated_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`order_no`
- `idx_createdTime`:created_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
