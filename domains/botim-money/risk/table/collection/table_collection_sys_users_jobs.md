---
id: tbl_collection_sys_users_jobs
object_type: Table
name: sys_users_jobs (sys_users_jobs)
aliases: [sys_users_jobs, collection.sys_users_jobs]
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

# sys_users_jobs (sys_users_jobs)

## 用途
物理表 `collection.sys_users_jobs`,主键 `user_id, job_id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `user_id` | bigint | 用户ID |
| `job_id` | bigint | 岗位ID |

## 主键 / 索引
- 主键:`user_id, job_id`
- `idx_job`:job_id

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
