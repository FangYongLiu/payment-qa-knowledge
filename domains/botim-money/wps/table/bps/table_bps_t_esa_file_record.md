---
id: tbl_bps_t_esa_file_record
object_type: Table
name: log table to record ESA file info (t_esa_file_record)
aliases: [t_esa_file_record, bps.t_esa_file_record]
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

# log table to record ESA file info (t_esa_file_record)

## 用途
物理表 `bps.t_esa_file_record`,主键 `id`。log table to record ESA file info。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | primary key |
| `file_name` | varchar(100) | Name of the file |
| `file_path` | varchar(128) | Path of the file |
| `file_type` | varchar(16) | Type of the file |
| `merchant_id` | char(32) | Merchant ID of the corresponding file |
| `status` | varchar(16) | Status of the file |
| `push_retry_times` | int | Retry times of the file |
| `pull_retry_times` | int | retry_times for pulling files · 可空 |
| `related_entity_id` | char(32) | Related entity ID |
| `created_at` | timestamp | created time |
| `updated_at` | timestamp | updated time |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
