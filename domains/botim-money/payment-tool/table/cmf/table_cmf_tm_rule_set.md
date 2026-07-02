---
id: tbl_cmf_tm_rule_set
object_type: Table
name: tm_rule_set (tm_rule_set)
aliases: [tm_rule_set, cmf.tm_rule_set]
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

# tm_rule_set (tm_rule_set)

## 用途
物理表 `cmf.tm_rule_set`,主键 `RULESET_ID, RULE_TABLE`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `RULESET_ID` | decimal(8) | 规则ID |
| `RULE_TABLE` | varchar(100) | 规则表 |
| `RULE_VALUE` | text | 规则内容 · 可空 |
| `INSERT_DATE` | timestamp | 插入日期 |
| `SQL_QUERY` | varchar(4000) | SQL查询 · 可空 |

## 主键 / 索引
- 主键:`RULESET_ID, RULE_TABLE`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
