---
id: tbl_cregister_t_report_analysis
object_type: Table
name: Batch Report Receipt File Analysis (t_report_analysis)
aliases: [t_report_analysis, cregister.t_report_analysis]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: cregister schema DDL
tags: [merchant-management, cregister]
sensitivity: normal
related_services: []
---

# Batch Report Receipt File Analysis (t_report_analysis)

## 用途
物理表 `cregister.t_report_analysis`,主键 `id`。Batch Report Receipt File Analysis。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | Primary Key ID · 可空 |
| `fund_provider_code` | varchar(24) | Channel Provider |
| `inst_code` | varchar(24) | Institution Code |
| `fund_channel_code` | varchar(24) | Channel Code |
| `file_name` | varchar(1024) | File Name · 可空 |
| `file_flag` | varchar(32) | UFS File Flag · 可空 |
| `version` | varchar(12) | File Version; Date format, used to determine which time"s file to download · 可空 |
| `status` | varchar(12) | Status; I-Init, D-Download, A-Analysis, S-Success, F-Failure |
| `gmt_create` | timestamp | Creation Time |
| `gmt_modified` | timestamp | Update Time |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
