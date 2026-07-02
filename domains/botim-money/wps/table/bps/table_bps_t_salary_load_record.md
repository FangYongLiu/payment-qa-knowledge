---
id: tbl_bps_t_salary_load_record
object_type: Table
name: salary load record (t_salary_load_record)
aliases: [t_salary_load_record, bps.t_salary_load_record]
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

# salary load record (t_salary_load_record)

## 用途
物理表 `bps.t_salary_load_record`,主键 `id`。salary load record。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | primary key |
| `txn_ref_no` | varchar(32) | txn ref no |
| `origin_id` | varchar(64) | origin id |
| `origin_bulk_id` | varchar(64) | origin bulk id |
| `payroll_bulk_id` | varchar(64) | payroll bulk id |
| `file_name` | varchar(128) | file name |
| `file_oss_path` | varchar(255) | file oss path |
| `sif_file_id` | varchar(100) | sif file id · 可空 |
| `sif_file_name` | varchar(100) | sif file name · 可空 |
| `status` | varchar(16) | status |
| `retry_times` | int | retry times |
| `createAt` | timestamp | create time |
| `updateAt` | timestamp | update time |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
