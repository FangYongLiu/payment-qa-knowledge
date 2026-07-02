---
id: tbl_bps_t_esa_file_record_detail
object_type: Table
name: log table to record ESA file details (t_esa_file_record_detail)
aliases: [t_esa_file_record_detail, bps.t_esa_file_record_detail]
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

# log table to record ESA file details (t_esa_file_record_detail)

## 用途
物理表 `bps.t_esa_file_record_detail`,主键 `id`。log table to record ESA file details。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | primary key |
| `esa_file_record_id` | char(32) | related esa file record id |
| `file_type` | varchar(16) | Type of the file |
| `merchant_id` | char(32) | Merchant ID of the corresponding file |
| `status` | varchar(16) | Status of the file |
| `business_id` | char(32) | business id of the corresponding file |
| `reason` | varchar(255) | reason of the file · 可空 |
| `line_number` | int | line number of the file · 可空 |
| `created_at` | timestamp | created time |
| `updated_at` | timestamp | updated time |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
