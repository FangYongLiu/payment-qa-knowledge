---
id: tbl_bps_t_bulk_parse_job
object_type: Table
name: Bulk file async parse progress job table (t_bulk_parse_job)
aliases: [t_bulk_parse_job, bps.t_bulk_parse_job]
domain: wps
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: bps schema DDL
tags: [wps, bps]
sensitivity: normal
related_services: []
---

# Bulk file async parse progress job table (t_bulk_parse_job)

## 用途
物理表 `bps.t_bulk_parse_job`,主键 `id`。Bulk file async parse progress job table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | varchar(64) | Application generated parse job ID |
| `bulk_type` | varchar(32) | Bulk business type, e.g. Employee or Payroll |
| `bulk_id` | varchar(64) | Related business bulk ID |
| `parse_status` | varchar(32) | Parse status: Init, Process, Success, Failed |
| `total_rows` | int | Total rows to parse |
| `processed_rows` | int | Rows already processed |
| `success_rows` | int | Rows parsed successfully |
| `failed_rows` | int | Rows failed during parse |
| `total_chunks` | int | Total parse chunks |
| `success_chunks` | int | Chunks parsed successfully |
| `failed_chunks` | int | Chunks failed during parse |
| `retry_count` | int | Parse retry count |
| `reason` | varchar(1024) | Failure reason or latest parse message · 可空 |
| `createAt` | datetime | Record creation time |
| `updateAt` | datetime | Record last update time |

## 主键 / 索引
- 主键:`id`
- `uk_bulk_parse_job_bulk`:bulk_type, bulk_id (UNIQUE)
- `idx_bulk_parse_job_status`:parse_status
- `idx_bulk_parse_job_update_at`:updateAt

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
