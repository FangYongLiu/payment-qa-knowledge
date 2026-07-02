---
id: tbl_transfer_t_exchange
object_type: Table
name: 币种转换表 (t_exchange)
aliases: [t_exchange, transfer.t_exchange]
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

# 币种转换表 (t_exchange)

## 用途
物理表 `transfer.t_exchange`,主键 `id`。币种转换表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(17) | 待补 |
| `voucher_no` | bigint(18) | 关联订单号 |
| `origin_currency` | varchar(10) | 源币种 |
| `origin_amount` | decimal(15, 4) | 源金额 |
| `dest_currency` | varchar(10) | 目标币种 |
| `dest_amount` | decimal(15, 4) | 目标金额 |
| `exchange_rate` | decimal(15, 4) | 汇率 · 可空 |
| `gmt_created` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
