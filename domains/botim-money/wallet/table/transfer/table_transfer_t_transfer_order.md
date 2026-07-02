---
id: tbl_transfer_t_transfer_order
object_type: Table
name: 备注 (t_transfer_order)
aliases: [t_transfer_order, transfer.t_transfer_order]
domain: wallet
status: active
owner: qianlong.wang
reviewer: qianlong.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: transfer schema DDL
tags: [wallet, transfer]
sensitivity: normal
related_services: []
---

# 备注 (t_transfer_order)

## 用途
物理表 `transfer.t_transfer_order`,主键 `payment_no`。备注。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `payment_no` | bigint(18) | 主键 |
| `out_trade_no` | varchar(64) | 商户转账订单 |
| `biz_product_code` | varchar(15) | 业务产品码 |
| `payer_uid` | varchar(32) | 付款人uid |
| `payer_mid` | varchar(32) | 付款人memberId |
| `partner_id` | varchar(32) | 商户号 |
| `gmt_paid` | timestamp | 付款时间 · 可空 |
| `payment_amount` | decimal(15, 4) | 付款金额 |
| `settled_amount` | decimal(15, 4) | 结算金额 |
| `refunded_amount` | decimal(15, 4) | 退款金额 |
| `currency` | varchar(10) | 币种 |
| `memo` | varchar | 待补 · 可空 |

## 主键 / 索引
- 主键:`payment_no`
- `idx_expire_time`:expire_time
- `idx_gmt_modified`:gmt_modified
- `idx_payer_mid`:payer_mid

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
