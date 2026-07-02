---
id: tbl_ccexchange_t_exchange_order
object_type: Table
name: 兑换订单 (t_exchange_order)
aliases: [t_exchange_order, ccexchange.t_exchange_order]
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

# 兑换订单 (t_exchange_order)

## 用途
物理表 `ccexchange.t_exchange_order`,主键 `id`。兑换订单。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id |
| `base_currency_code` | varchar(32) | 本位币币种 |
| `base_amount` | decimal(23, 8) | 本位币金额 |
| `quote_amount` | decimal(23, 8) | 报价金额 |
| `quote_currency_code` | varchar(32) | 报价币种 |
| `request_time` | timestamp(3) | 请求时间 |
| `symbol` | varchar(32) | symbol |
| `direction` | varchar(16) | 买卖方向 |
| `merchant_mid` | varchar(32) | merchantMid |
| `status` | varchar(32) | status |
| `fail_message` | varchar(128) | 错误原因 · 可空 |
| `fail_code` | varchar(32) | 错误码 · 可空 |
| `unity_result_code` | varchar(64) | 统一结果码 · 可空 |
| `created_time` | timestamp(3) | 创建时间 |
| `last_updated_time` | timestamp(3) | 最后更新时间 |
| `data_version` | bigint | 数据版本 |
| `channel_exa_order_id` | bigint | 兑换订单号 · 可空 |
| `customer_mid` | varchar(32) | customerMid · 可空 |

## 主键 / 索引
- 主键:`id`
- `i_eo_ct`:created_time
- `i_eo_lut`:last_updated_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
