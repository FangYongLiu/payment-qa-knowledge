---
id: tbl_credit_t_cs_risk_level
object_type: Table
name: risk level (t_cs_risk_level)
aliases: [t_cs_risk_level, credit.t_cs_risk_level]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: credit schema DDL
tags: [lending, credit]
sensitivity: normal
related_services: []
---

# risk level (t_cs_risk_level)

## 用途
物理表 `credit.t_cs_risk_level`,主键 `id`。risk level。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 主键 · 可空 |
| `risk_tag` | varchar(50) | risk tag |
| `criteria` | varchar(1000) | criteria info |
| `price_level` | varchar(64) | baseline,midiumHigh,high,low |
| `version` | smallint(5) | version |
| `order_status` | smallint(5) | NEW 0 , AGAIN 1, RENEW 2 |
| `period` | varchar (30) | period [1, 2, 3] |
| `ext` | varchar(50) | ext · 可空 |
| `status` | smallint(5) | offline or online |
| `created_time` | timestamp | create time · 可空 |
| `last_modified` | timestamp | modified time · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
