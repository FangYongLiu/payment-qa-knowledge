---
id: tbl_personal_t_task_manager
object_type: Table
name: 任务管理表 (t_task_manager)
aliases: [t_task_manager, personal.t_task_manager]
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: personal schema DDL
tags: [activation, personal]
sensitivity: normal
related_services: []
---

# 任务管理表 (t_task_manager)

## 用途
物理表 `personal.t_task_manager`,主键 `id`。任务管理表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主键 · 可空 |
| `task_type` | varchar(32) | 任务类型 |
| `relate_key` | varchar(64) | 任务关联Key |
| `expire_time` | timestamp | 到期时间 |
| `gmt_created` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`id`
- `uk_relate_key_task_type`:relate_key, task_type (UNIQUE)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
