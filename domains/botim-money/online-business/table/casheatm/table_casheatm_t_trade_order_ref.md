---
id: tbl_casheatm_t_trade_order_ref
object_type: Table
name: 中台交易订单引用 (t_trade_order_ref)
aliases: [t_trade_order_ref, casheatm.t_trade_order_ref]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: casheatm schema DDL
tags: [online-business, casheatm]
sensitivity: normal
related_services: []
---

# 中台交易订单引用 (t_trade_order_ref)

## 用途
物理表 `casheatm.t_trade_order_ref`,主键 `id`。中台交易订单引用。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 交易订单号 |
| `acq_order_id` | bigint | 收单订单号 |
| `acq_partner_id` | varchar(50) | 收单平台号 |
| `acq_mht_order_no` | varchar(200) | 收单商户订单号 |
| `acq_subject` | varchar(200) | 收单标题 · 可空 |
| `acq_merchant_name` | varchar(200) | 收单商户名 · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
