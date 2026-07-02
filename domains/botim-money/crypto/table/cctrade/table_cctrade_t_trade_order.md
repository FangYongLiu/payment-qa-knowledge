---
id: tbl_cctrade_t_trade_order
object_type: Table
name: 交易订单 (t_trade_order)
aliases: [t_trade_order, cctrade.t_trade_order]
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

# 交易订单 (t_trade_order)

## 用途
物理表 `cctrade.t_trade_order`,主键 `id`。交易订单。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id |
| `subject` | varchar(200) | 标题 |
| `product_code` | varchar(32) | 产品码 |
| `partner_id` | varchar(32) | partner_id |
| `clearing_code` | varchar(32) | 清分码 |
| `currency_code` | varchar(32) | 提币币种 |
| `amount` | decimal(23, 8) | 提币金额 |
| `status` | varchar(32) | status |
| `expired_time` | timestamp(3) | 超时时间 |
| `trade_precision` | int | trade_precision |
| `fail_message` | varchar(128) | 错误原因 · 可空 |
| `fail_code` | varchar(32) | 错误码 · 可空 |
| `unity_result_code` | varchar(64) | 统一结果码 · 可空 |
| `created_time` | timestamp(3) | 创建时间 |
| `last_updated_time` | timestamp(3) | 最后更新时间 |
| `data_version` | bigint | 数据版本 |
| `voucher_no` | varchar(32) | 凭证号 · 可空 |

## 主键 / 索引
- 主键:`id`
- `i_to_ct`:created_time
- `i_to_lut`:last_updated_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
