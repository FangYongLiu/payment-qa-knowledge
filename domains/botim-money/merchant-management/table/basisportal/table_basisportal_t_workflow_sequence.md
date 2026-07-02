---
id: tbl_basisportal_t_workflow_sequence
object_type: Table
name: node sequence in workflow (t_workflow_sequence)
aliases: [t_workflow_sequence, basisportal.t_workflow_sequence]
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

# node sequence in workflow (t_workflow_sequence)

## 用途
物理表 `basisportal.t_workflow_sequence`,主键 `id`。node sequence in workflow。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(21) | 待补 |
| `workflow_id` | bigint(21) | workflow ID |
| `version` | varchar(16) | version |
| `source_node` | varchar(32) | source node key · 可空 |
| `target_node` | varchar(32) | target node key · 可空 |
| `expression` | varchar(255) | help choose sequece · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
