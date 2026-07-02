---
id: tbl_basisportal_t_ru_task
object_type: Table
name: runtime task (t_ru_task)
aliases: [t_ru_task, basisportal.t_ru_task]
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

# runtime task (t_ru_task)

## 用途
物理表 `basisportal.t_ru_task`,主键 `id`。runtime task。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(21) | 待补 |
| `instance_id` | bigint(21) | instance ID |
| `node_name` | varchar(32) | node name · 可空 |
| `node_key` | varchar(32) | workflow node key |
| `last_node_key` | varchar(32) | last node key · 可空 |
| `begin_time` | timestamp | begin time · 可空 |
| `sign_type` | tinyint | 1-single-sign 2-Countersign · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_t_ru_task_instance_id`:instance_id

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
