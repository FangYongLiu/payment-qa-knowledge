---
id: tbl_cctrade_t_trade_refund_order
object_type: Table
name: 退款订单 (t_trade_refund_order)
aliases: [t_trade_refund_order, cctrade.t_trade_refund_order]
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

# 退款订单 (t_trade_refund_order)

## 用途
物理表 `cctrade.t_trade_refund_order`,主键 `id`。退款订单。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id |
| `trade_order_id` | bigint | 交易订单号 |
| `payee_mid` | varchar(32) | 收款人 |
| `currency_code` | varchar(32) | 提币币种 |
| `amount` | decimal(23, 8) | 提币金额 |
| `status` | varchar(32) | status |
| `reason` | varchar(200) | 退款原因 · 可空 |
| `fail_message` | varchar(128) | 错误原因 · 可空 |
| `fail_code` | varchar(32) | 错误码 · 可空 |
| `unity_result_code` | varchar(64) | 统一结果码 · 可空 |
| `created_time` | timestamp(3) | 创建时间 |
| `last_updated_time` | timestamp(3) | 最后更新时间 |
| `data_version` | bigint | 数据版本 |
| `voucher_no` | varchar(32) | 凭证号 · 可空 |

## 主键 / 索引
- 主键:`id`
- `i_tro_ct`:created_time
- `i_tro_lut`:last_updated_time
- `i_tro_toi`:trade_order_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
