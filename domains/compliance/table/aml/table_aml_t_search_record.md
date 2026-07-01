---
id: tbl_aml_t_search_record
object_type: Table
domain: compliance
status: active
owner: dewen.li
reviewer: dewen.li
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (aml schema) 2026-06-25
tags:
- aml
- aml
- t_search_record
subdomain: aml
module: null
sensitivity: normal
name: 名称模糊搜索记录表(t_search_record)
aliases:
- t_search_record
related_services:
- svc_aml
related_scenarios: []
---
# 名称模糊搜索记录表(t_search_record)

## 用途
名称模糊搜索记录表。属 aml 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int | PK / AUTO_INC |  |
| `search_file_name` | varchar(100) | NOT NULL | 搜索文件名 |
| `search_file_path` | varchar(255) | NOT NULL | 搜索文件路径 |
| `upload_time` | timestamp | NOT NULL | 上传时间 |
| `finish_time` | timestamp |  | 搜索完成时间 |
| `result_file_name` | varchar(100) |  | 结果文件名 |
| `result_file_path` | varchar(100) |  | 结果文件路径 |
| `upload_user` | varchar(50) | NOT NULL | 上传文件用户 |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
