---
id: tbl_adg_t_pdf_file_tracker
object_type: Table
name: Tracks PDF files associated with applications and users (t_pdf_file_tracker)
aliases: [t_pdf_file_tracker, adg.t_pdf_file_tracker]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: adg schema DDL
tags: [marketing, adg]
sensitivity: normal
related_services: []
---

# Tracks PDF files associated with applications and users (t_pdf_file_tracker)

## 用途
物理表 `adg.t_pdf_file_tracker`,主键 `id`。Tracks PDF files associated with applications and users。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | Unique identifier, primary key · 可空 |
| `app_code` | varchar(31) | Application code |
| `file_id` | varchar(127) | Unique identifier for the PDF file |
| `file_type` | varchar(32) | Type of the PDF file (e.g., invoice, report, contract) |
| `create_time` | timestamp | Record creation timestamp |
| `update_time` | timestamp | Record last update timestamp |

## 主键 / 索引
- 主键:`id`
- `uk_file_id_app_code_file_type`:file_id, app_code, file_type (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
