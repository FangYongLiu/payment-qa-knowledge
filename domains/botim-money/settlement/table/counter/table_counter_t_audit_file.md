---
id: tbl_counter_t_audit_file
object_type: Table
name: 审核附件表 (t_audit_file)
aliases: [t_audit_file, counter.t_audit_file]
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: counter schema DDL
tags: [settlement, counter]
sensitivity: normal
related_services: []
---

# 审核附件表 (t_audit_file)

## 用途
物理表 `counter.t_audit_file`,主键 `file_id`。审核附件表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `file_id` | bigint(17) | 待补 |
| `audit_id` | bigint(17) | 审核ID · 可空 |
| `file_name` | varchar(64) | 文件名称 · 可空 |
| `file_url` | varchar(128) | 文件路径 · 可空 |
| `file_type` | varchar(8) | 文件类型 · 可空 |
| `is_apply` | varchar(8) | 文件来源,经办/复核 · 可空 |
| `gmt_create` | timestamp | 创建时间 · 可空 |
| `log_id` | bigint(17) | 审核日志ID |

## 主键 / 索引
- 主键:`file_id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
