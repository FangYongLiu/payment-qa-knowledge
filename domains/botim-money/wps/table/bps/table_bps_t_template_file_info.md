---
id: tbl_bps_t_template_file_info
object_type: Table
name: payroll load to wps account refund record (t_template_file_info)
aliases: [t_template_file_info, bps.t_template_file_info]
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

# payroll load to wps account refund record (t_template_file_info)

## 用途
物理表 `bps.t_template_file_info`,主键 `id`。payroll load to wps account refund record。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | primary key |
| `template_file_type` | varchar(32) | template file type |
| `template_name` | varchar(100) | template name |
| `file_oss_path` | varchar(128) | file oss path |
| `file_name` | varchar(100) | file name |
| `file_suffix` | char(10) | file suffix |
| `file_url` | varchar(128) | file url · 可空 |
| `createAt` | timestamp | create time |
| `updateAt` | timestamp | update time |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
