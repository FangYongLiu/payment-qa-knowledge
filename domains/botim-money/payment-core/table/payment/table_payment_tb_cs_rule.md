---
id: tbl_payment_tb_cs_rule
object_type: Table
name: 清算规则 (tb_cs_rule)
aliases: [tb_cs_rule, payment.tb_cs_rule]
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

# 清算规则 (tb_cs_rule)

## 用途
物理表 `payment.tb_cs_rule`,主键 `RULE_ID`。清算规则。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `RULE_ID` | bigint | 规则ID · 可空 |
| `RULE_NAME` | varchar(64) | 规则名称 |
| `PRODUCT_CODE` | varchar(16) | 产品码 · 可空 |
| `PAYMENT_TYPE` | char(2) | 支付类型 |
| `CLEARING_CODE` | varchar(32) | 清算代码 |
| `REQUEST_TYPE` | varchar(16) | 请求类型 |
| `SESSION_LEVEL` | varchar(8) | 层次，大类前缀：O-外场；I-内场 |
| `SESSION_TYPE` | char | 场次类型：R-实时；T-定时任务触发； |
| `SESSION_TEMPLATE_ID` | decimal(11) | 场次模板ID · 可空 |
| `CAN_SET_DELAY` | char | 是否允许外部定义延时：Y-允许；N-不允许 · 可空 |
| `SUMMARY_TEMPLATE` | varchar(128) | 摘要模板 · 可空 |
| `STATUS` | char | 状态。I-初始；E-生效；U-失效 |
| `extension` | varchar(255) | extension · 可空 |
| `GMT_MODIFIED` | timestamp | 最后修改时间 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `MEMO` | varchar(128) | 备注 · 可空 |

## 主键 / 索引
- 主键:`RULE_ID`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
