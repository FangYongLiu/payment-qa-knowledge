---
id: tbl_amlreport_tc_etl_result
object_type: Table
name: etl result table (tc_etl_result)
aliases: [tc_etl_result, amlreport.tc_etl_result]
domain: compliance
status: active
owner: dewen.li
reviewer: dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: amlreport schema DDL
tags: [compliance, amlreport]
sensitivity: normal
related_services: []
---

# etl result table (tc_etl_result)

## 用途
物理表 `amlreport.tc_etl_result`,主键 `id`。etl result table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id · 可空 |
| `data_type` | varchar(60) | data type  EID_LIMIT  · 可空 |
| `etl_dt` | char(8) | etl date yyyyMMdd · 可空 |
| `bigdata_finish_time` | timestamp | bigdata finish time · 可空 |
| `handle_finish_time` | timestamp | handle finish time · 可空 |
| `status` | char | status I-init  P-processing  S-success  F-fail  · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
