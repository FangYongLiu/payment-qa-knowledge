---
id: tbl_bps_t_file_info
object_type: Table
name: file info (t_file_info)
aliases: [t_file_info, bps.t_file_info]
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

# file info (t_file_info)

## 用途
物理表 `bps.t_file_info`,主键 `id`。file info。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | primary key |
| `file_oss_path` | varchar(255) | file oss path · 可空 |
| `file_name` | varchar(128) | 文件名 |
| `file_suffix` | char(10) | file suffix |
| `file_size` | bigint(32) | file size |
| `file_url` | varchar(255) | file download url · 可空 |
| `maker_id` | varchar(64) | maker id |
| `employee_id` | varchar(64) | employee id · 可空 |
| `merchant_id` | varchar(64) | merchant id |
| `createAt` | timestamp | create time |
| `updateAt` | timestamp | update time |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
