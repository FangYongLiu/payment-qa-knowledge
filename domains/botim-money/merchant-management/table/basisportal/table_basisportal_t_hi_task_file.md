---
id: tbl_basisportal_t_hi_task_file
object_type: Table
name: archive files uploaded by approver (t_hi_task_file)
aliases: [t_hi_task_file, basisportal.t_hi_task_file]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: basisportal schema DDL
tags: [merchant-management, basisportal]
sensitivity: normal
related_services: []
---

# archive files uploaded by approver (t_hi_task_file)

## 用途
物理表 `basisportal.t_hi_task_file`,主键 `id`。archive files uploaded by approver。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(21) | 待补 |
| `hi_operation_id` | bigint(21) | history task operation id |
| `file_name` | varchar(64) | file name |
| `file_url` | varchar(128) | ufs url |
| `file_size` | int | file size · 可空 |
| `create_by` | varchar(45) | account of operator · 可空 |
| `create_time` | timestamp | upload time · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_t_hi_task_file_hi_operation_id`:hi_operation_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
