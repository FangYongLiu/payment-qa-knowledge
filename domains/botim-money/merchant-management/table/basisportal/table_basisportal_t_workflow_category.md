---
id: tbl_basisportal_t_workflow_category
object_type: Table
name: The register category of external system (t_workflow_category)
aliases: [t_workflow_category, basisportal.t_workflow_category]
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

# The register category of external system (t_workflow_category)

## 用途
物理表 `basisportal.t_workflow_category`,主键 `id`。The register category of external system。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(21) | 待补 |
| `system_code` | varchar(32) | code of external system · 可空 |
| `category` | varchar(64) | category of audit · 可空 |
| `data_form_url` | varchar(100) | URL of Global Data Form · 可空 |
| `workflow_interface` | varchar(255) | Full name of interface invoke by workflow · 可空 |
| `register_time` | timestamp | register time · 可空 |
| `update_time` | timestamp | Update Time · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
