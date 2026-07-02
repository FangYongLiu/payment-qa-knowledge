---
id: tbl_cregister_t_register_batch_order
object_type: Table
name: Merchant Registration Batch (t_register_batch_order)
aliases: [t_register_batch_order, cregister.t_register_batch_order]
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

# Merchant Registration Batch (t_register_batch_order)

## 用途
物理表 `cregister.t_register_batch_order`,主键 `batch_id`。Merchant Registration Batch。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `batch_id` | bigint | Batch Id; 8+9 |
| `batch_no` | varchar(32) | Batch Number |
| `relation_batch_id` | bigint | Related ID; This batch can only be processed after the related batch is completed · 可空 |
| `inst_code` | varchar(24) | Institution Code |
| `fund_channel_code` | varchar(24) | Channel Code |
| `fund_provider_code` | varchar(24) | Channel Provider |
| `fund_channel_api` | varchar(12) | Channel API |
| `total_count` | int | Total Count of This Batch; Initially 0 |
| `success_count` | int | Success Count; Initially 0 |
| `fail_count` | int | Fail Count; Initially 0 |
| `is_locked` | char | Lock; N,Y, Initially N (unlocked) |
| `gmt_archive` | timestamp | Archive Time |
| `query_times` | int(5) | Query Times; Initially 0 |
| `gmt_next_retry` | timestamp | Next Retry Query Result Time · 可空 |
| `start_time` | datetime | Start Time · 可空 |
| `end_time` | datetime | End Time · 可空 |
| `file_name` | varchar(1024) | File Name · 可空 |
| `file_tag` | varchar(80) | UFS File Tag; Use commas to separate if multiple files need to be generated · 可空 |
| `back_file_name` | varchar(1024) | Back File Name · 可空 |
| `back_file_tag` | varchar(80) | UFS Back File Tag · 可空 |
| `status` | char | Status: A - To be Archived, I - Sending, S - Submitted, R - Returned, E - Processing Error, F - Submission Failed |
| `register_type` | varchar(16) | Registration Type; MERCHANT: Merchant, STORE: Store, DEVICE: Device · 可空 |
| `unity_code` | varchar(32) | Unified Error Code · 可空 |
| `extension` | varchar(1024) | Extension Information · 可空 |
| `memo` | varchar(100) | Remark · 可空 |
| `gmt_create` | timestamp | Creation Time |
| `gmt_modified` | timestamp | Update Time |

## 主键 / 索引
- 主键:`batch_id`
- `idx_batch_no`:batch_no
- `idx_create_time`:gmt_create

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
