---
id: tbl_bps_t_branch_corporate_source_bulk
object_type: Table
name: Branch corporate bulk registration metadata (t_branch_corporate_source_bulk)
aliases: [t_branch_corporate_source_bulk, bps.t_branch_corporate_source_bulk]
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

# Branch corporate bulk registration metadata (t_branch_corporate_source_bulk)

## 用途
物理表 `bps.t_branch_corporate_source_bulk`,主键 `id`。Branch corporate bulk registration metadata。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | ULID primary key |
| `request_type` | varchar(50) | Request type (e.g., ADD, UPDATE) |
| `total_quantity` | int | Total number of records in bulk |
| `success_quantity` | int | Number of successful records |
| `fail_quantity` | int | Number of failed records |
| `file_id` | char(32) | Uploaded file ID · 可空 |
| `maker_id` | varchar(32) | User who created the bulk |
| `merchant_mid` | varchar(32) | Merchant MID (parent corporate) |
| `submit_date` | timestamp | Date when bulk was submitted · 可空 |
| `status` | varchar(10) | Bulk status: Processing, Completed, Failed |
| `reason` | varchar(255) | Failure reason if status is Failed · 可空 |
| `createAt` | timestamp | Created timestamp |
| `updateAt` | timestamp | Updated timestamp |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
