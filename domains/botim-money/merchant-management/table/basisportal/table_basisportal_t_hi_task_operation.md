---
id: tbl_basisportal_t_hi_task_operation
object_type: Table
name: assignee operation history (t_hi_task_operation)
aliases: [t_hi_task_operation, basisportal.t_hi_task_operation]
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

# assignee operation history (t_hi_task_operation)

## 用途
物理表 `basisportal.t_hi_task_operation`,主键 `id`。assignee operation history。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(21) | 待补 |
| `hi_task_id` | bigint(21) | history task id |
| `assignee` | varchar(45) | account of approver |
| `operate` | tinyint | operate or not: 0-no 1-yes · 可空 |
| `operate_time` | timestamp | operate time · 可空 |
| `result` | tinyint | approval result: 1-approved 2-rejected · 可空 |
| `remarks` | varchar(512) | remarks · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_t_hi_task_operation_assignee`:assignee
- `idx_t_hi_task_operation_hi_task_id`:hi_task_id

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
