---
id: tbl_basisportal_t_workflow_node
object_type: Table
name: nodes in workflow (t_workflow_node)
aliases: [t_workflow_node, basisportal.t_workflow_node]
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

# nodes in workflow (t_workflow_node)

## 用途
物理表 `basisportal.t_workflow_node`,主键 `id`。nodes in workflow。业务语义细节**待补**(表结构来自 DDL)。

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
| `node_key` | varchar(32) | identifier in workflow |
| `name` | varchar(32) | Node Name |
| `sign_type` | tinyint | 1-single-sign 2-Countersign · 可空 |
| `data_form_type` | tinyint(1) | 1-inherit global 2-custom · 可空 |
| `data_form_url` | varchar(128) | URL of business data form · 可空 |
| `business_handler` | varchar(255) | full name of business data hanlder · 可空 |
| `node_order` | int(8) | node sort in workflow · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_t_workflow_node_workflow_id`:workflow_id

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
