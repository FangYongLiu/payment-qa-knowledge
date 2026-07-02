---
id: tbl_ccacquire_t_refund_order
object_type: Table
name: 退款订单 (t_refund_order)
aliases: [t_refund_order, ccacquire.t_refund_order]
domain: crypto
status: active
owner: can.wang
reviewer: can.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ccacquire schema DDL
tags: [crypto, ccacquire]
sensitivity: normal
related_services: []
---

# 退款订单 (t_refund_order)

## 用途
物理表 `ccacquire.t_refund_order`,主键 `global_id`。退款订单。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `global_id` | bigint | 退款全局号 |
| `request_no` | varchar(200) | 等同于requestIdentity.requestNo.查询方便 |
| `partner_id` | varchar(200) | 发起方memberId |
| `device_id` | varchar(200) | 发起方设备id · 可空 |
| `acquire_global_id` | bigint | 收单全局号 |
| `currency_code` | varchar(32) | 收单币种 |
| `amount` | decimal(23, 8) | 收单金额 |
| `reason` | varchar(500) | 原因 · 可空 |
| `notify_url` | varchar(500) | 商户通知地址 · 可空 |
| `status` | varchar(200) | 待补 |
| `operator_name` | varchar(200) | 待补 · 可空 |
| `fail_code` | varchar(50) | 错误码 · 可空 |
| `fail_message` | varchar(200) | 错误描述 · 可空 |
| `estimated_time` | timestamp(3) | 预期时间 · 可空 |
| `created_time` | timestamp(3) | 创建时间 |
| `last_updated_time` | timestamp(3) | 最后更新时间 |
| `data_version` | bigint | 数据版本 |
| `unity_result_code` | varchar(200) | 统一结果码 · 可空 |
| `settled_time` | timestamp(3) | 退结算时间 · 可空 |
| `finished_time` | timestamp(3) | 退款成功时间 · 可空 |
| `payee_fee_amount` | decimal(23, 8) | 退款手续费 · 可空 |
| `payee_fee_currency` | varchar(32) | 退款手续费币种 · 可空 |
| `settlement_amount` | decimal(23, 8) | 结算金额 · 可空 |
| `settlement_currency` | varchar(32) | 结算币种 · 可空 |
| `reverted` | varchar(10) | 待补 · 可空 |
| `refund_usage` | varchar(16) | 退款用途 · 可空 |
| `refund_type` | varchar(16) | 待补 · 可空 |
| `reserved` | varchar(200) | 待补 · 可空 |
| `pfbt_crcy` | varchar(50) | payeeFeeAmountBeforeTaxCurrencyCode · 可空 |
| `pfbt_amt` | decimal(19, 4) | payeeFeeAmountBeforeTax · 可空 |
| `pfv_crcy` | varchar(50) | payeeFeeVatCurrencyCode · 可空 |
| `pf_vat` | decimal(19, 4) | payeeFeeVat · 可空 |

## 主键 / 索引
- 主键:`global_id`
- `i_ao_ag`:acquire_global_id
- `i_ao_ft`:finished_time
- `i_ao_lut`:last_updated_time
- `i_ao_st`:settled_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
