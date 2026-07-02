---
id: tbl_ccdeposit_t_customer_deposit_order
object_type: Table
name: 客户充值订单 (t_customer_deposit_order)
aliases: [t_customer_deposit_order, ccdeposit.t_customer_deposit_order]
domain: crypto
status: active
owner: can.wang
reviewer: can.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ccdeposit schema DDL
tags: [crypto, ccdeposit]
sensitivity: normal
related_services: []
---

# 客户充值订单 (t_customer_deposit_order)

## 用途
物理表 `ccdeposit.t_customer_deposit_order`,主键 `id`。客户充值订单。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id |
| `fee_amount_crcy` | varchar(32) | 手续费币种 |
| `fee_amount` | decimal(23, 8) | 手续费金额 |
| `settle_amount_crcy` | varchar(32) | 结算币种 |
| `settle_amount` | decimal(23, 8) | 结算金额 |
| `deposit_amount_crcy` | varchar(32) | 充值币种 |
| `deposit_amount` | decimal(23, 8) | 充值金额 |
| `notification_url` | varchar(128) | 回调地址 · 可空 |
| `member_id` | varchar(32) | 用户MID |
| `status` | varchar(32) | status |
| `event_id` | varchar(50) | 事件id · 可空 |
| `chain_code` | varchar(32) | 链代码 · 可空 |
| `tx_hash` | varchar(200) | txid · 可空 |
| `payer_address` | varchar(128) | 付款钱包地址 · 可空 |
| `receiver_address` | varchar(128) | 收款钱包地址 · 可空 |
| `customer_id` | varchar(200) | 客户ID |
| `fail_message` | varchar(128) | 错误原因 · 可空 |
| `fail_code` | varchar(32) | 错误码 · 可空 |
| `unity_result_code` | varchar(64) | 统一结果码 · 可空 |
| `confirmed_time` | timestamp(3) | 确认时间 |
| `created_time` | timestamp(3) | 创建时间 |
| `last_updated_time` | timestamp(3) | 最后更新时间 |
| `data_version` | bigint | 数据版本 |

## 主键 / 索引
- 主键:`id`
- `i_do_ct`:confirmed_time
- `i_do_lut`:last_updated_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
