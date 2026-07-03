---
id: tbl_casheatm_t_cash_top_up_order
object_type: Table
name: cash topup 订单 (t_cash_top_up_order)
aliases: [t_cash_top_up_order, casheatm.t_cash_top_up_order]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: casheatm schema DDL
tags: [online-business, casheatm]
sensitivity: normal
related_services: [svc_cash_eatm]
---

# cash topup 订单 (t_cash_top_up_order)

## 用途
物理表 `casheatm.t_cash_top_up_order`,主键 `global_id`。cash topup 订单。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `global_id` | bigint | 退款全局号 |
| `trade_order_id` | bigint | 交易订单号 |
| `device_id` | bigint | 设备id |
| `currency_code` | varchar(50) | 收单币种代码 |
| `amount` | decimal(19, 4) | 收单金额 |
| `merchant_mid` | varchar(50) | 收款人mid |
| `business_type` | varchar(50) | 业务类型 · 可空 |
| `customer_mobile` | varchar(50) | 客户手机 · 可空 |
| `payment_order_id` | bigint | 支付订单号 · 可空 |
| `status` | varchar(50) | 状态 |
| `fail_code` | varchar(200) | 错误码 · 可空 |
| `unity_result_code` | varchar(200) | 统一结果码 · 可空 |
| `created_time` | timestamp(3) | 创建时间 |
| `last_updated_time` | timestamp(3) | 最后更新时间 |
| `data_version` | bigint | 数据版本 |
| `paid_time` | timestamp(3) | 支付时间 · 可空 |
| `operator_id` | varchar(32) | 操作员ID · 可空 |
| `pay_channel` | varchar(64) | pay_channel · 可空 |

## 主键 / 索引
- 主键:`global_id`
- `i_ci_ct`:created_time
- `i_ci_lut`:last_updated_time
- `i_trd_dev`:trade_order_id, device_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
