---
id: tbl_bps_t_request_yse_record
object_type: Table
name: request yse record (t_request_yse_record)
aliases: [t_request_yse_record, bps.t_request_yse_record]
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

# request yse record (t_request_yse_record)

## 用途
物理表 `bps.t_request_yse_record`,主键 `id`。request yse record。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | primary key |
| `txn_ref_no` | varchar(64) | txnRefNo |
| `request_ref_no` | varchar(32) | request ref no · 可空 |
| `file_id` | varchar(32) | batch id · 可空 |
| `request_api` | varchar(16) | yse api key |
| `data` | varchar(255) | request data · 可空 |
| `main_field_name` | varchar(32) | main field name · 可空 |
| `main_field_data` | varchar(64) | main field data · 可空 |
| `code` | varchar(10) | response code |
| `message` | varchar(255) | response message · 可空 |
| `memo` | varchar(128) | memo · 可空 |
| `createAt` | timestamp | create time |
| `updateAt` | timestamp | update time |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
