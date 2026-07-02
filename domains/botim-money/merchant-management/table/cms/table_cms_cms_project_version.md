---
id: tbl_cms_cms_project_version
object_type: Table
name: 项目版本表 (cms_project_version)
aliases: [cms_project_version, cms.cms_project_version]
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

# 项目版本表 (cms_project_version)

## 用途
物理表 `cms.cms_project_version`,主键 `id`。项目版本表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(19) | 主键 · 可空 |
| `project_code` | varchar(50) | 项目编码 |
| `project_version` | varchar(20) | 项目版本 |
| `description` | varchar(255) | 描述 · 可空 |
| `status` | varchar(10) | 状态 · 可空 |
| `create_time` | timestamp | 创建时间 · 可空 |
| `create_user` | varchar(32) | 创建人 · 可空 |
| `update_time` | timestamp | 修改时间 · 可空 |
| `update_user` | varchar(32) | 修改人 · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
