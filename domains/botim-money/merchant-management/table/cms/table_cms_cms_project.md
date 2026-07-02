---
id: tbl_cms_cms_project
object_type: Table
name: 项目表 (cms_project)
aliases: [cms_project, cms.cms_project]
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

# 项目表 (cms_project)

## 用途
物理表 `cms.cms_project`,主键 `id`。项目表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主键 · 可空 |
| `project_code` | varchar(50) | 项目编码 |
| `name` | varchar(32) | 项目名称 |
| `host_app` | varchar(20) | 载体 |
| `platform` | varchar(10) | app类型 |
| `status` | varchar(10) | 状态 |
| `description` | varchar(500) | 描述 · 可空 |
| `create_time` | timestamp | 创建时间 · 可空 |
| `create_user` | varchar(32) | 创建人 · 可空 |
| `update_time` | timestamp | 修改时间 · 可空 |
| `update_user` | varchar(32) | 修改人 · 可空 |

## 主键 / 索引
- 主键:`id`
- `uk_project_code`:project_code (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
