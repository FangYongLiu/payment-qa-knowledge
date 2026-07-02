---
id: tbl_basisportal_t_workflow_node_assign
object_type: Table
name: candidate of workflow node (t_workflow_node_assign)
aliases: [t_workflow_node_assign, basisportal.t_workflow_node_assign]
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

# candidate of workflow node (t_workflow_node_assign)

## 用途
物理表 `basisportal.t_workflow_node_assign`,主键 `id`。candidate of workflow node。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(21) | 待补 |
| `workflow_id` | bigint(21) | Workflow ID · 可空 |
| `version` | varchar(16) | Version No · 可空 |
| `node_key` | varchar(30) | Node Key |
| `assign_method` | tinyint | 1-role, 2-permission, 3-user, 4-rule · 可空 |
| `object_key` | varchar(45) | ID of role,permission,rule Or account of user · 可空 |
| `object_name` | varchar(64) | object name · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
