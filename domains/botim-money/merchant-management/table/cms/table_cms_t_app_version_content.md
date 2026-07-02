---
id: tbl_cms_t_app_version_content
object_type: Table
name: app更新文案表 (t_app_version_content)
aliases: [t_app_version_content, cms.t_app_version_content]
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

# app更新文案表 (t_app_version_content)

## 用途
物理表 `cms.t_app_version_content`,主键 `id`。app更新文案表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(18) | 主键 · 可空 |
| `version_id` | varchar(20) | 版本号 |
| `sequence` | int | 文案序列、顺序 |
| `description` | varchar(4096) | 文案内容 |
| `lang_type` | varchar(120) | 语言类型 · 可空 |
| `gmt_created` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
