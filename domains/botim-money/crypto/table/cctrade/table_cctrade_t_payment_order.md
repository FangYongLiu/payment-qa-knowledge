---
id: tbl_cctrade_t_payment_order
object_type: Table
name: 支付订单 (t_payment_order)
aliases: [t_payment_order, cctrade.t_payment_order]
domain: crypto
status: active
owner: can.wang
reviewer: can.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: cctrade schema DDL
tags: [crypto, cctrade]
sensitivity: normal
related_services: []
---

# 支付订单 (t_payment_order)

## 用途
物理表 `cctrade.t_payment_order`,主键 `id`。支付订单。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id |
| `type` | varchar(32) | 订单类型 |
| `trade_order_id` | bigint | 交易订单id |
| `payer_mid` | varchar(32) | 订单类型 · 可空 |
| `status` | varchar(32) | status |
| `fail_message` | varchar(128) | 错误原因 · 可空 |
| `fail_code` | varchar(32) | 错误码 · 可空 |
| `unity_result_code` | varchar(64) | 统一结果码 · 可空 |
| `paid_time` | timestamp(3) | 最后更新时间 · 可空 |
| `created_time` | timestamp(3) | 创建时间 |
| `last_updated_time` | timestamp(3) | 最后更新时间 |
| `data_version` | bigint | 数据版本 |
| `payment_voucher_no` | varchar(32) | 支付凭证号 · 可空 |
| `platform_id` | varchar(32) | 付款人平台ID · 可空 |

## 主键 / 索引
- 主键:`id`
- `i_po_ct`:created_time
- `i_po_lut`:last_updated_time
- `i_po_trd`:trade_order_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
