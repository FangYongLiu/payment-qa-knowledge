---
id: tbl_offlinepay_t_refund_order
object_type: Table
name: Refund Order (t_refund_order)
aliases: [t_refund_order, offlinepay.t_refund_order]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: offlinepay schema DDL
tags: [payment-core, offlinepay]
sensitivity: normal
related_services: []
---

# Refund Order (t_refund_order)

## 用途
物理表 `offlinepay.t_refund_order`,主键 `global_id`。Refund Order。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `global_id` | bigint | global_id |
| `amount` | decimal(19, 4) | amount · 可空 |
| `amount_currency` | char(3) | amount_currency · 可空 |
| `payment_order_id` | bigint | payment_order_id |
| `status` | varchar(16) | status · 可空 |
| `trace` | bigint | trace · 可空 |
| `type` | varchar(32) | values:PRE_CLEARING、POST_SETTLEMENT、PENDING_SETTLEMENT · 可空 |
| `channel_code` | varchar(32) | channel_code · 可空 |
| `device_id` | bigint | device_id · 可空 |
| `fail_code` | varchar(16) | fail_code · 可空 |
| `fail_message` | varchar(128) | fail_message · 可空 |
| `partner_id` | varchar(32) | partner_id · 可空 |
| `rrn` | varchar(128) | 待补 · 可空 |
| `created_time` | timestamp(3) | created_time |
| `last_updated_time` | timestamp(3) | last_updated_time |
| `data_version` | bigint | data_version |

## 主键 / 索引
- 主键:`global_id`
- `uk_rrn`:rrn (UNIQUE)
- `i_ro_ct`:created_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
