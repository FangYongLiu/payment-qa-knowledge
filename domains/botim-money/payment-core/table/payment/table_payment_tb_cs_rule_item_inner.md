---
id: tbl_payment_tb_cs_rule_item_inner
object_type: Table
name: 清算规则内场条款 (tb_cs_rule_item_inner)
aliases: [tb_cs_rule_item_inner, payment.tb_cs_rule_item_inner]
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

# 清算规则内场条款 (tb_cs_rule_item_inner)

## 用途
物理表 `payment.tb_cs_rule_item_inner`,主键 `ITEM_ID`。清算规则内场条款。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `ITEM_ID` | bigint | 条款ID · 可空 |
| `RULE_ID` | decimal(11) | 规则ID |
| `SUITE_NO` | decimal(5) | 套号 |
| `PARTY_ROLE` | varchar(16) | 参与角色 |
| `DEFAULT_ACCOUNT` | varchar(32) | 默认账户号 · 可空 |
| `DC_DIRECTION` | char | 借贷方向：D-借；C-贷 |
| `PRICING_TYPE` | varchar(16) | 计价类型：EXPRESSION-表达式；OTHERSIDE-对方 |
| `PRICING_EXPRESSION` | varchar(128) | 计价表达式 · 可空 |
| `match_expression` | varchar(255) | expression (velocity) · 可空 |
| `FUND_PROP` | char(2) | 资金属性：CA-贷记资金 DA-借记资金 BI-借贷皆可 PD-依赖渠道资金属性 · 可空 |
| `FREEZE_TAG` | char | 冻结标记：F-冻结；N-正常 · 可空 |
| `RED_BLUE_TAG` | char | 红蓝标记 · 可空 |
| `CHANNEL_ACCOUNT_TYPE` | char | 渠道帐号类型：W-待清算；B-银存 · 可空 |
| `GMT_MODIFIED` | timestamp | 最后修改时间 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `MEMO` | varchar(128) | 备注 · 可空 |

## 主键 / 索引
- 主键:`ITEM_ID`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
