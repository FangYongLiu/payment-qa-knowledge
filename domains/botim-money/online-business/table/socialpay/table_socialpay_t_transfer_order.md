---
id: tbl_socialpay_t_transfer_order
object_type: Table
name: 转账订单 (t_transfer_order)
aliases: [t_transfer_order, socialpay.t_transfer_order]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: socialpay schema DDL
tags: [online-business, socialpay]
sensitivity: normal
related_services: [svc_socialpay]
---

# 转账订单 (t_transfer_order)

## 用途
物理表 `socialpay.t_transfer_order`,主键 `id`。转账订单。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(10) | 待补 · 可空 |
| `out_trade_no` | varchar(64) | 外部订单号 |
| `voucher_no` | varchar(32) | 交易订单号 |
| `partner_id` | varchar(32) | 商户号 |
| `transfer_type` | varchar(20) | 转账类型 |
| `payer_identity` | varchar(32) | 付款人标示 |
| `payer_member_id` | varchar(32) | 付款人member_id |
| `payer_account_type` | varchar(16) | 付款方账户类型 · 可空 |
| `card_id` | varchar(20) | 卡id · 可空 |
| `payee_identity` | varchar(32) | 收款人标示 · 可空 |
| `payee_member_id` | varchar(32) | 收款人会员Id · 可空 |
| `payee_account_type` | varchar(16) | 收款人账户类型 · 可空 |
| `amount` | decimal(19, 4) | 金额 |
| `currency` | varchar(10) | 币种 |
| `expire_time` | timestamp | 过期时间 · 可空 |
| `status` | varchar(20) | 状态：WAIT_PAY、PAY_SUCCESS、TRADE_FINISH、TRADE_FAILED、 |
| `receive_time` | timestamp | 领取时间 · 可空 |
| `refunded_time` | timestamp | 退款时间 · 可空 |
| `notify_param` | varchar(400) | 通知透传参数 · 可空 |
| `gmt_created` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 更新时间 |
| `memo` | varchar(100) | 备注 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_tro_out_trade_no`:out_trade_no (UNIQUE)
- `idx_tro_voucher_no`:voucher_no

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
