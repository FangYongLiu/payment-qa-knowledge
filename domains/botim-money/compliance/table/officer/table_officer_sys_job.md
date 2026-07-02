---
id: tbl_officer_sys_job
object_type: Table
name: post (sys_job)
aliases: [sys_job, officer.sys_job]
domain: compliance
status: active
owner: dewen.li
reviewer: dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: officer schema DDL
tags: [compliance, officer]
sensitivity: normal
related_services: []
---

# post (sys_job)

## 用途
物理表 `officer.sys_job`,主键 `job_id`。post。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `job_id` | bigint | ID · 可空 |
| `name` | varchar(255) | Position name |
| `enabled` | tinyint | Job status |
| `job_sort` | int | Sorting · 可空 |
| `create_by` | varchar(100) | creator · 可空 |
| `update_by` | varchar(100) | Updater · 可空 |
| `create_time` | timestamp | Creation date · 可空 |
| `update_time` | timestamp | Update time · 可空 |

## 主键 / 索引
- 主键:`job_id`
- `uk_uniq_name`:name (UNIQUE)
- `inx_enabled`:enabled

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
