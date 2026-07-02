---
id: tbl_basisportal_t_ru_task_assignee
object_type: Table
name: task assignee (t_ru_task_assignee)
aliases: [t_ru_task_assignee, basisportal.t_ru_task_assignee]
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

# task assignee (t_ru_task_assignee)

## 用途
物理表 `basisportal.t_ru_task_assignee`,主键 `id`。task assignee。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(21) | 待补 |
| `task_id` | bigint(21) | task ID · 可空 |
| `assignee` | varchar(45) | account of approver · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_t_ru_task_assignee_task_id`:task_id

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
