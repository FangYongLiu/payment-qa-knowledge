---
id: tbl_basisportal_t_hi_task
object_type: Table
name: task history (t_hi_task)
aliases: [t_hi_task, basisportal.t_hi_task]
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

# task history (t_hi_task)

## 用途
物理表 `basisportal.t_hi_task`,主键 `id`。task history。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(21) | 待补 |
| `instance_id` | bigint(21) | instance id |
| `node_key` | varchar(32) | node key |
| `node_name` | varchar(32) | Current node name · 可空 |
| `last_node_key` | varchar(32) | last node key · 可空 |
| `next_node_key` | varchar(32) | next node key · 可空 |
| `sign_type` | tinyint | 1-single-sign 2-Countersign · 可空 |
| `begin_time` | timestamp | task begin time · 可空 |
| `end_time` | timestamp | task end time · 可空 |
| `result` | tinyint | 1-pass 0-rejected · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_t_hi_task_instance_id`:instance_id

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
