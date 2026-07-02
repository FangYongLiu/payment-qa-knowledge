---
id: tbl_memberfront_t_pay_order
object_type: Table
name: 支付订单表 (t_pay_order)
aliases: [t_pay_order, memberfront.t_pay_order]
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: memberfront schema DDL
tags: [activation, memberfront]
sensitivity: normal
related_services: []
---

# 支付订单表 (t_pay_order)

## 用途
物理表 `memberfront.t_pay_order`,主键 `voucher_no`。支付订单表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `voucher_no` | bigint(32) | 支付订单号 |
| `oder_no` | bigint(32) | 转账订单号 |
| `amount` | decimal(19, 4) | 转账金额 |
| `currency` | varchar(25) | 币种 |
| `partner_id` | varchar(32) | 平台ID · 可空 |
| `status` | varchar(25) | 状态 |
| `trade_status` | varchar(32) | 交易状态 |
| `finish_time` | timestamp | 转账完成时间 · 可空 |
| `payee_member_id` | varchar(32) | 收款人 · 可空 |
| `payee_account_type` | varchar(20) | 收款账户类型 · 可空 |
| `payee_account_no` | varchar(64) | 收款账户号 · 可空 |
| `payer_member_id` | varchar(32) | 付款人会员编号 |
| `payer_account_type` | varchar(30) | 付款账户类型 |
| `extension` | varchar(255) | 拓展字段 · 可空 |
| `memo` | varchar(255) | 备注 · 可空 |
| `create_time` | timestamp | 建立时间 |
| `update_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`voucher_no`
- `idx_front_payorder_updatetime`:update_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
