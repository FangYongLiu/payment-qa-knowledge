---
id: tbl_cmf_tr_fc_target_inst_relation
object_type: Table
name: tr_fc_target_inst_relation (tr_fc_target_inst_relation)
aliases: [tr_fc_target_inst_relation, cmf.tr_fc_target_inst_relation]
domain: payment-tool
status: active
owner: kingo.liang
reviewer: kingo.liang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: cmf schema DDL
tags: [payment-tool, cmf]
sensitivity: normal
related_services: []
---

# tr_fc_target_inst_relation (tr_fc_target_inst_relation)

## 用途
物理表 `cmf.tr_fc_target_inst_relation`,主键 `ID`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `ID` | int unsigned | ID · 可空 |
| `FUND_CHANNEL_CODE` | varchar(32) | 编码 |
| `TARGET_INST_CODE` | varchar(16) | 目标机构代码 · 可空 |
| `TARGET_INST_NAME` | varchar(32) | 目标机构名称 · 可空 |
| `SCORE` | mediumint(5) | 比分 · 可空 |
| `MIN` | decimal(5, 2) | 最小值 · 可空 |
| `MAX` | decimal(5, 2) | 最大值 · 可空 |
| `ABILITY` | tinyint | 支付能力 : 1-能支付，2-不能支付 · 可空 |
| `CURRENCY` | char(3) | 币种 · 可空 |

## 主键 / 索引
- 主键:`ID`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
