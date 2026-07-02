---
id: tbl_ccexchange_t_channel_exchange_order
object_type: Table
name: 渠道兑换订单 (t_channel_exchange_order)
aliases: [t_channel_exchange_order, ccexchange.t_channel_exchange_order]
domain: crypto
status: active
owner: can.wang
reviewer: can.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ccexchange schema DDL
tags: [crypto, ccexchange]
sensitivity: normal
related_services: []
---

# 渠道兑换订单 (t_channel_exchange_order)

## 用途
物理表 `ccexchange.t_channel_exchange_order`,主键 `id`。渠道兑换订单。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id |
| `status` | varchar(32) | status |
| `actual_base_crcy` | varchar(32) | 实际本位币币种 · 可空 |
| `actual_base_amt` | decimal(23, 8) | 实际本位币金额 · 可空 |
| `actual_quote_amt` | decimal(23, 8) | 实际报价金额 · 可空 |
| `actual_quote_crcy` | varchar(32) | 实际报价币种 · 可空 |
| `direction` | varchar(16) | 买卖方向 |
| `symbol` | varchar(32) | symbol |
| `expected_base_crcy` | varchar(32) | 预期本位币币种 |
| `expected_base_amt` | decimal(23, 8) | 预期本位币金额 |
| `expected_quote_amt` | decimal(23, 8) | 预期报价金额 |
| `expected_quote_crcy` | varchar(32) | 预期报价币种 |
| `channel_type` | varchar(32) | 待补 |
| `merchant_mid` | varchar(32) | merchantMid |
| `fail_message` | varchar(128) | 错误原因 · 可空 |
| `fail_code` | varchar(32) | 错误码 · 可空 |
| `unity_result_code` | varchar(64) | 统一结果码 · 可空 |
| `created_time` | timestamp(3) | 创建时间 |
| `last_updated_time` | timestamp(3) | 最后更新时间 |
| `data_version` | bigint | 数据版本 |
| `exchange_usage` | varchar(32) | 兑换用途 · 可空 |

## 主键 / 索引
- 主键:`id`
- `i_ceo_ct`:created_time
- `i_ceo_lut`:last_updated_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
