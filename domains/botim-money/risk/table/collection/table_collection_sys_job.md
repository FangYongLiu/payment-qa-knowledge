---
id: tbl_collection_sys_job
object_type: Table
name: 岗位 (sys_job)
aliases: [sys_job, collection.sys_job]
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: collection schema DDL
tags: [risk, collection]
sensitivity: normal
related_services: []
---

# 岗位 (sys_job)

## 用途
物理表 `collection.sys_job`,主键 `job_id`。岗位。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `job_id` | bigint | ID · 可空 |
| `name` | varchar(255) | 岗位名称 |
| `enabled` | tinyint(5) | 岗位状态 |
| `job_sort` | int(5) | 排序 · 可空 |
| `create_by` | varchar(100) | 创建者 · 可空 |
| `update_by` | varchar(100) | 更新者 · 可空 |
| `create_time` | timestamp | 创建日期 · 可空 |
| `update_time` | timestamp | 更新时间 · 可空 |
| `start_days` | smallint(5) | 帐龄起始时间 · 可空 |
| `end_days` | smallint(5) | 帐龄结束时间 · 可空 |
| `is_keep` | tinyint | 是否保持原催收员0:否 1:是 · 可空 |
| `type` | tinyint | 1岗位2帐龄 · 可空 |
| `pid` | smallint(5) | 上级岗位id · 可空 |

## 主键 / 索引
- 主键:`job_id`
- `uk_uniq_name`:name (UNIQUE)
- `inx_enabled`:enabled

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
