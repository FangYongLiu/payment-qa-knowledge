---
id: tbl_ccacquire_t_payment_info
object_type: Table
name: 收单数据 (t_payment_info)
aliases: [t_payment_info, ccacquire.t_payment_info]
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

# 收单数据 (t_payment_info)

## 用途
物理表 `ccacquire.t_payment_info`,主键 `global_id`。收单数据。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `global_id` | bigint | 全局号 |
| `pay_channel` | varchar(200) | 支付渠道 · 可空 |
| `payer_mid` | varchar(200) | 付款人mid · 可空 |
| `payer_fee_currency_code` | varchar(32) | 收单币种 · 可空 |
| `payer_fee_amount` | decimal(23, 8) | 收单金额 · 可空 |
| `payee_fee_currency_code` | varchar(32) | 结算币种 · 可空 |
| `payee_fee_amount` | decimal(23, 8) | 结算金额 · 可空 |
| `paid_currency_code` | varchar(32) | 付款币种 · 可空 |
| `paid_amount` | decimal(19, 4) | 付款金额 · 可空 |
| `paid_time` | timestamp(3) | 支付成功时间 · 可空 |
| `settlement_currency_code` | varchar(50) | 结算币种 · 可空 |
| `settlement_amount` | decimal(19, 4) | 结算金额 · 可空 |
| `settled_time` | timestamp(3) | 结算时间 · 可空 |
| `pfbt_crcy` | varchar(16) | 不含税金额币种 · 可空 |
| `pfbt_amt` | decimal(23, 8) | 不含税金额 · 可空 |
| `pfv_crcy` | varchar(16) | vat税币种 · 可空 |
| `pf_vat` | decimal(23, 8) | vat税 · 可空 |
| `created_time` | timestamp(3) | 创建时间 |
| `last_updated_time` | timestamp(3) | 最后更新时间 |
| `data_version` | bigint | 数据版本 |

## 主键 / 索引
- 主键:`global_id`
- `i_ao_pt`:paid_time
- `i_ao_st`:settled_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
