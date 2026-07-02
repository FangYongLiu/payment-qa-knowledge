---
id: tbl_transfer_t_paymethod
object_type: Table
name: 付款方式 (t_paymethod)
aliases: [t_paymethod, transfer.t_paymethod]
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

# 付款方式 (t_paymethod)

## 用途
物理表 `transfer.t_paymethod`,主键 `id`。付款方式。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(17) | 主键 |
| `payment_no` | bigint(18) | 付款订单主键 |
| `pay_channel` | varchar(32) | 支付渠道 |
| `pay_scene` | varchar(20) | 支付场景 |
| `amount` | decimal(15, 4) | 金额 |
| `currency` | varchar(10) | 币种 |
| `payment_info` | varchar(100) | 支付信息 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
