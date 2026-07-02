---
id: tbl_transfer_t_cancel_order
object_type: Table
name: 撤销订单 (t_cancel_order)
aliases: [t_cancel_order, transfer.t_cancel_order]
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

# 撤销订单 (t_cancel_order)

## 用途
物理表 `transfer.t_cancel_order`,主键 `cancel_no`。撤销订单。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `cancel_no` | bigint(18) | 主键 |
| `out_cancel_no` | varchar(64) | 商户撤销订单 |
| `payment_no` | bigint(18) | 付款订单号 · 可空 |
| `settle_no` | bigint(18) | 结算订单号 · 可空 |
| `partner_id` | varchar(32) | 商户号 |
| `amount` | decimal(15, 4) | 金额 |
| `currency` | varchar(10) | 币种 |
| `status` | varchar(20) | 状态 |
| `cancel_type` | varchar(15) | 撤销类型：SINGLE-单笔撤销,ALL - 多笔撤销 |
| `memo` | varchar(100) | 备注 · 可空 |
| `cancel_flag` | varchar(20) | 退款标识 手动：MANUAL、自动：AUTO · 可空 |
| `gmt_created` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`cancel_no`
- `uk_can_out_cancel_no`:out_cancel_no (UNIQUE)
- `idx_gmt_modified`:gmt_modified
- `idx_payment_no`:payment_no

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
