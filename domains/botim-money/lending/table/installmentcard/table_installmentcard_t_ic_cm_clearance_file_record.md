---
id: tbl_installmentcard_t_ic_cm_clearance_file_record
object_type: Table
name: Clearance file generation and tracking records (t_ic_cm_clearance_file_record)
aliases: [t_ic_cm_clearance_file_record, installmentcard.t_ic_cm_clearance_file_record]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: installmentcard schema DDL
tags: [lending, installmentcard]
sensitivity: normal
related_services: []
---

# Clearance file generation and tracking records (t_ic_cm_clearance_file_record)

## 用途
物理表 `installmentcard.t_ic_cm_clearance_file_record`,主键 `id`。Clearance file generation and tracking records。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key · 可空 |
| `file_type` | tinyint | File type as integer enum (TINYINT). Example mapping: 0=ACCEPT |
| `file_date` | date | Business date the file covers (e.g., yesterday) |
| `data_range_start` | datetime | Start of the data range included in the file |
| `data_range_end` | datetime | End of the data range included in the file |
| `file_name` | varchar(127) | Generated file name (e.g., I_IC_20260408_1712345678.txt) · 可空 |
| `ufs_file_tag` | varchar(255) | UFS file tag/path returned after upload, used to retrieve the file later · 可空 |
| `upload_status` | tinyint | Upload status as integer enum (TINYINT). Example mapping: 0=PENDING, 1=UPLOADED, 2=UPLOAD_FAILED |
| `send_status` | tinyint | Send status to clearance team as integer enum (TINYINT). Example mapping: 0=NOT_SENT, 1=SENT, 2=SEND_FAILED |
| `record_count` | int | Total number of records included in the file |
| `error_message` | varchar(500) | Error details if upload or send failed · 可空 |
| `created_at` | datetime | Record creation time |
| `updated_at` | datetime | Record last update time |

## 主键 / 索引
- 主键:`id`
- `uk_file_date_type`:file_date, file_type (UNIQUE)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
