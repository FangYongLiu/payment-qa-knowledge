---
id: tbl_outman_tm_route_rule_factor
object_type: Table
name: factor规则表 (tm_route_rule_factor)
aliases: [tm_route_rule_factor, outman.tm_route_rule_factor]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: outman schema DDL
tags: [payment-core, outman]
sensitivity: normal
related_services: []
---

# factor规则表 (tm_route_rule_factor)

## 用途
物理表 `outman.tm_route_rule_factor`,主键 `FACTOR_ID`。factor规则表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `FACTOR_ID` | bigint(32) | 路由编号 |
| `FACTOR_NAME` | varchar(64) | factor_name |
| `FILTER_ID` | decimal(11) | filter_id |
| `TARGET` | varchar(256) | 目标 |
| `MATCH_EXPRESSION` | varchar(1024) | 匹配表达式 · 可空 |
| `DEFAULT_WEIGHT` | decimal(11) | 默认权重 |
| `CALC_WEIGHT` | decimal(11) | 匹配表达式的计算权重 · 可空 |
| `MEMO` | varchar(256) | memo · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 更新时间 · 可空 |
| `OPERATOR` | varchar(32) | 创建人 · 可空 |
| `CONFIRM_OPERATOR` | varchar(32) | 审核人 · 可空 |
| `UPDATE_OPERATROR` | varchar(32) | 修改人 · 可空 |
| `OPERATOR2` | varchar(32) | 创建人 · 可空 |
| `CONFIRM_OPERATOR2` | varchar(32) | 审核人 · 可空 |
| `UPDATE_OPERATROR2` | varchar(32) | 修改人 · 可空 |

## 主键 / 索引
- 主键:`FACTOR_ID`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
