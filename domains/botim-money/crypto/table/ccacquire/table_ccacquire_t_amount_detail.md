---
id: tbl_ccacquire_t_amount_detail
object_type: Table
name: 金额信息 (t_amount_detail)
aliases: [t_amount_detail, ccacquire.t_amount_detail]
domain: crypto
status: active
owner: can.wang
reviewer: can.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ccacquire schema DDL
tags: [crypto, ccacquire]
sensitivity: normal
related_services: []
---

# 金额信息 (t_amount_detail)

## 用途
物理表 `ccacquire.t_amount_detail`,主键 `global_id`。金额信息。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `global_id` | bigint | 全局号 |
| `amount` | decimal(23, 8) | 待补 · 可空 |
| `currency_code` | varchar(32) | 币种 · 可空 |
| `discountable_amount` | decimal(23, 8) | 待补 · 可空 |
| `discountable_currency_code` | varchar(32) | 币种 · 可空 |
| `tip_amount` | decimal(23, 8) | 待补 · 可空 |
| `tip_currency_code` | varchar(32) | 币种 · 可空 |
| `vat_amount` | decimal(23, 8) | 待补 · 可空 |
| `vat_currency_code` | varchar(32) | 币种 · 可空 |

## 主键 / 索引
- 主键:`global_id`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
