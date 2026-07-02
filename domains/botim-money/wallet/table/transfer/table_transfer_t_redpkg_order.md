---
id: tbl_transfer_t_redpkg_order
object_type: Table
name: 主题 (t_redpkg_order)
aliases: [t_redpkg_order, transfer.t_redpkg_order]
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

# 主题 (t_redpkg_order)

## 用途
物理表 `transfer.t_redpkg_order`,主键 `redpkg_no`。主题。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `redpkg_no` | bigint(18) | 主键 |
| `out_trade_no` | varchar(64) | 商户红包单号 |
| `partner_id` | varchar(32) | 商户ID |
| `payment_no` | bigint(18) | 付款单号 |
| `amount` | decimal(15, 4) | 金额 |
| `currency` | varchar(10) | 币种 |
| `type` | varchar(20) | 红包类型：AVERAGE,LUCKY,PERSONAL |
| `subject` | varchar | 待补 · 可空 |

## 主键 / 索引
- 主键:`redpkg_no`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
