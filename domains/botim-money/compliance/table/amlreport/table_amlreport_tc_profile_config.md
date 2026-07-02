---
id: tbl_amlreport_tc_profile_config
object_type: Table
name: 画像数据同步策略配置 (tc_profile_config)
aliases: [tc_profile_config, amlreport.tc_profile_config]
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

# 画像数据同步策略配置 (tc_profile_config)

## 用途
物理表 `amlreport.tc_profile_config`,主键 `id`。画像数据同步策略配置。业务语义细节**待补**(表结构来自 DDL)。

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
| `key_col` | varchar(32) | 画像key对应的字段 · 可空 |
| `policy` | varchar(1024) | 字段同步策略 · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
