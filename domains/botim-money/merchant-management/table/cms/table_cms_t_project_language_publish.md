---
id: tbl_cms_t_project_language_publish
object_type: Table
name: 项目语言发布表 (t_project_language_publish)
aliases: [t_project_language_publish, cms.t_project_language_publish]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: cms schema DDL
tags: [merchant-management, cms]
sensitivity: normal
related_services: []
---

# 项目语言发布表 (t_project_language_publish)

## 用途
物理表 `cms.t_project_language_publish`,主键 `id`。项目语言发布表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(18) | 主键 · 可空 |
| `project_code` | varchar(50) | 项目code |
| `language_type` | varchar(32) | 语言类型 |
| `language_url` | varchar(500) | 语言包路径 |
| `is_publish` | varchar(10) | 是否发布 · 可空 |
| `publish_time` | timestamp | 发布时间 · 可空 |
| `version` | int | 版本 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
