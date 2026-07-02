---
id: tbl_basisportal_t_workflow
object_type: Table
name: definition of workflow (t_workflow)
aliases: [t_workflow, basisportal.t_workflow]
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

# definition of workflow (t_workflow)

## 用途
物理表 `basisportal.t_workflow`,主键 `id`。definition of workflow。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(21) | 待补 |
| `system_code` | varchar(32) | code of registered system |
| `category` | varchar(64) | audit type |
| `cur_version` | varchar(16) | active version · 可空 |
| `status` | tinyint(1) | 0-disabled 1-enabled · 可空 |
| `has_config` | tinyint(1) | 0-disabled 1-enabled · 可空 |
| `remarks` | varchar(255) | Remarks · 可空 |
| `create_by` | varchar(45) | account of creator · 可空 |
| `create_time` | timestamp | create time · 可空 |
| `update_by` | varchar(45) | account of modifier · 可空 |
| `update_time` | timestamp | update time · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_t_workflow_system_code`:system_code

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
