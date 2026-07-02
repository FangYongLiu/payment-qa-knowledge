---
id: tbl_payment_tb_cs_rule_item_outer
object_type: Table
name: 清结算条款外场 (tb_cs_rule_item_outer)
aliases: [tb_cs_rule_item_outer, payment.tb_cs_rule_item_outer]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: payment schema DDL
tags: [payment-core, payment]
sensitivity: normal
related_services: []
---

# 清结算条款外场 (tb_cs_rule_item_outer)

## 用途
物理表 `payment.tb_cs_rule_item_outer`,主键 `ITEM_ID`。清结算条款外场。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `ITEM_ID` | bigint | 条款ID · 可空 |
| `RULE_ID` | decimal(11) | 规则ID |
| `PARTY_ROLE` | varchar(16) | 参与角色 |
| `PRICING_EXPRESSION` | varchar(128) | 计价表达式 |
| `GMT_MODIFIED` | timestamp | 最后修改时间 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `MEMO` | varchar(128) | 备注 · 可空 |

## 主键 / 索引
- 主键:`ITEM_ID`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
