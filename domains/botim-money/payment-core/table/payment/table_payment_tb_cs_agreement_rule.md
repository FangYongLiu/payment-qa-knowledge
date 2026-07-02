---
id: tbl_payment_tb_cs_agreement_rule
object_type: Table
name: 协议规则关系 (tb_cs_agreement_rule)
aliases: [tb_cs_agreement_rule, payment.tb_cs_agreement_rule]
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

# 协议规则关系 (tb_cs_agreement_rule)

## 用途
物理表 `payment.tb_cs_agreement_rule`,主键 `RELATION_ID`。协议规则关系。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `RELATION_ID` | decimal(11) | 关系ID |
| `RULE_ID` | decimal(11) | 规则ID |
| `AGREEMENT_ID` | decimal(11) | 协议ID，主键:SEQ_CLEARING_AGREEMENT |
| `GMT_CREATE` | timestamp | 创建时间 |

## 主键 / 索引
- 主键:`RELATION_ID`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
