---
id: tbl_amlreport_tc_profile_result
object_type: Table
name: 画像数据同步结果 (tc_profile_result)
aliases: [tc_profile_result, amlreport.tc_profile_result]
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

# 画像数据同步结果 (tc_profile_result)

## 用途
物理表 `amlreport.tc_profile_result`,主键 `id`。画像数据同步结果。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 主键 |
| `profile_result_name` | varchar(64) | 画像结果表 · 可空 |
| `profile_code` | varchar(128) | 画像编号 · 可空 |
| `bigdata_finish_time` | timestamp | 大数据同步数据完成时间 · 可空 |
| `dataeden_finish_time` | timestamp | 向dataEden同步数据完成时间 · 可空 |
| `status` | tinyint | 状态 1启用 0停用 · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
