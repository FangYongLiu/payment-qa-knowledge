---
id: tbl_payment_tb_ps_cs_rule_relation
object_type: Table
name: 支付服务清算规则关系表 (tb_ps_cs_rule_relation)
aliases: [tb_ps_cs_rule_relation, payment.tb_ps_cs_rule_relation]
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

# 支付服务清算规则关系表 (tb_ps_cs_rule_relation)

## 用途
物理表 `payment.tb_ps_cs_rule_relation`,主键 `CR_ID`。支付服务清算规则关系表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `CR_ID` | bigint | 主键 · 可空 |
| `PS_ID` | decimal(15) | 流程配置ID · 可空 |
| `CLEARING_CODE` | varchar(32) | 清算代码 |
| `REQUEST_TYPE` | varchar(16) | 请求类型 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 最后修改时间 |
| `MEMO` | varchar(128) | 备注 · 可空 |
| `EXPRESSION` | varchar(256) | 执行条件,现在用velocity表达式 · 可空 |

## 主键 / 索引
- 主键:`CR_ID`
- `UIDX_CS_PS`:PS_ID, CLEARING_CODE, REQUEST_TYPE

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
