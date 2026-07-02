---
id: tbl_offlinepay_t_fund_bucket
object_type: Table
name: Fund Bucket (t_fund_bucket)
aliases: [t_fund_bucket, offlinepay.t_fund_bucket]
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

# Fund Bucket (t_fund_bucket)

## 用途
物理表 `offlinepay.t_fund_bucket`,主键 `global_id`。Fund Bucket。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `global_id` | bigint | global_id |
| `clear_amount` | decimal(19, 4) | clear_amount · 可空 |
| `clear_amount_cur` | char(3) | clear_amount_currency · 可空 |
| `settled_mcht_amt` | decimal(19, 4) | settled_merchant_amount · 可空 |
| `settled_mcht_amt_cur` | char(3) | settled_merchant_amount_currency · 可空 |
| `settling_amount` | decimal(19, 4) | settling_amount · 可空 |
| `settling_amount_cur` | char(3) | settling_amount_currency · 可空 |
| `settled_fee_amount` | decimal(19, 4) | settled_fee_amount · 可空 |
| `settled_fee_amt_cur` | char(3) | settled_fee_amount_currency · 可空 |
| `refunding_amount` | decimal(19, 4) | refunding_amount · 可空 |
| `refunding_amt_cur` | char(3) | refunding_amount_currency · 可空 |
| `refunded_amount` | decimal(19, 4) | refunded_amount · 可空 |
| `refunded_amt_cur` | char(3) | refunded_amount_currency · 可空 |
| `pending_amount` | decimal(19, 4) | pending_amount · 可空 |
| `pending_amt_cur` | char(3) | pending_amount_currency · 可空 |
| `payment_amount` | decimal(19, 4) | payment_amount · 可空 |
| `payment_amt_cur` | char(3) | payment_amount_currency · 可空 |
| `reversed` | char | reversed · 可空 |
| `created_time` | timestamp(3) | created_time |
| `last_updated_time` | timestamp(3) | last_updated_time |
| `data_version` | bigint | data_version |

## 主键 / 索引
- 主键:`global_id`
- `i_fb_ct`:created_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
