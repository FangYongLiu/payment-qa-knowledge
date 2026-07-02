---
id: tbl_cregister_t_register_batch_result
object_type: Table
name: Merchant Batch Registration Result (t_register_batch_result)
aliases: [t_register_batch_result, cregister.t_register_batch_result]
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

# Merchant Batch Registration Result (t_register_batch_result)

## 用途
物理表 `cregister.t_register_batch_result`,主键 `result_id`。Merchant Batch Registration Result。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `result_id` | bigint | Primary Key ID |
| `batch_id` | bigint | Batch ID |
| `fund_provider_code` | varchar(24) | Channel Provider |
| `fund_channel_code` | varchar(24) | Channel Code |
| `inst_code` | varchar(24) | Institution Code |
| `fund_channel_api` | varchar(12) | Channel API |
| `batch_type` | varchar(12) | Batch Type; FILE, INTERFACE |
| `total_count` | int | Total Count |
| `success_count` | int | Success Count |
| `fail_count` | int | Fail Count |
| `status` | char | Status; F：FINISH， I：Pending |
| `memo` | varchar(100) | Remark · 可空 |
| `gmt_create` | timestamp | Creation Time |
| `gmt_modified` | timestamp | Update Time |

## 主键 / 索引
- 主键:`result_id`
- `idx_batch_id`:batch_id

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
