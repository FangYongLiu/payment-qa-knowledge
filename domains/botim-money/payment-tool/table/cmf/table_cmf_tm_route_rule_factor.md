---
id: tbl_cmf_tm_route_rule_factor
object_type: Table
name: 资金渠道路由要素 (tm_route_rule_factor)
aliases: [tm_route_rule_factor, cmf.tm_route_rule_factor]
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

# 资金渠道路由要素 (tm_route_rule_factor)

## 用途
物理表 `cmf.tm_route_rule_factor`,主键 `FACTOR_ID`。资金渠道路由要素。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `FACTOR_ID` | int unsigned | 要素ID · 可空 |
| `FACTOR_NAME` | varchar(32) | 要素名称 |
| `FACTOR_WEIGHT` | decimal(3) | 要素权重 |
| `EXPRESSION_TYPE` | char | 表达式类型：G（groovy），V（velocity） |
| `EXPRESSION_CONTENT` | varchar(1024) | 评分表达式内容 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 最后修改时间 |
| `MEMO` | varchar(128) | 备注 · 可空 |
| `FACTOR_CODE` | varchar(32) | 要素代码 · 可空 |
| `FUND_CHANNEL_CODE` | varchar(32) | 资金渠道代码 · 可空 |
| `API_CODE` | varchar(48) | API编码 · 可空 |

## 主键 / 索引
- 主键:`FACTOR_ID`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
