---
id: tbl_upic_t_transaction_order_extend
object_type: Table
name: 记账订单扩展 (t_transaction_order_extend)
aliases: [t_transaction_order_extend, upic.t_transaction_order_extend]
domain: card
status: active
owner: jianfei.wang
reviewer: jianfei.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: upic schema DDL
tags: [card, upic]
sensitivity: normal
related_services: []
---

# 记账订单扩展 (t_transaction_order_extend)

## 用途
物理表 `upic.t_transaction_order_extend`,主键 `trx_voucher_no`。记账订单扩展。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `trx_voucher_no` | bigint | 交易扩展凭证 凭证服务产生 |
| `upi_flow_id` | varchar(50) | 记账流水id |
| `message_id` | varchar(50) | 记账消息id · 可空 |
| `transaction_type` | varchar(10) | 记账类型：DEBIT=借记，CREDIT=贷记，REVERSAL=冲正 |
| `token` | varchar(32) | token · 可空 |
| `merchant_id` | varchar(32) | 商户id · 可空 |
| `merchant_name` | varchar(128) | 商户名称 · 可空 |
| `transaction_currency` | char(3) | 交易币种 |
| `transaction_amount` | decimal(19, 4) | 交易金额：已减去折扣金额 |
| `discount_details` | varchar(255) | 折扣信息 · 可空 |
| `bill_amount` | decimal(19, 4) | 账单金额 |
| `bill_currency` | char(3) | 账单币种 |
| `bill_conversion_rate` | decimal(19, 8) | Bill Conversion Rate |
| `settle_amount` | decimal(19, 4) | 结算金额 |
| `settle_currency` | char(3) | 结算币种 |
| `settle_conversion_rate` | decimal(19, 8) | Settle Conversion Rate |
| `settle_date` | timestamp | 结算日期 · 可空 |
| `pos_entry_mode_code` | varchar(10) | Point Of Service Entry Mode Code · 可空 |
| `conversion_date` | varchar(10) | 汇率日期 · 可空 |
| `transaction_note` | varchar(128) | 交易备注 · 可空 |
| `extension` | varchar(255) | 扩展参数 · 可空 |
| `memo` | varchar(255) | 备注 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`trx_voucher_no`
- `idx_message_id`:message_id
- `idx_update_time`:update_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
