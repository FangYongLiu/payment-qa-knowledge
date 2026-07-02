---
id: tbl_cms_t_config_template_field
object_type: Table
name: 模版属性表 (t_config_template_field)
aliases: [t_config_template_field, cms.t_config_template_field]
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

# 模版属性表 (t_config_template_field)

## 用途
物理表 `cms.t_config_template_field`,主键 `id`。模版属性表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 待补 · 可空 |
| `field` | varchar(50) | 属性 |
| `name` | varchar(50) | 简称 |
| `type` | varchar(20) | 字段类型 |
| `memo` | varchar(255) | 字段描述 · 可空 |
| `required` | char | 是否必填 |
| `gmt_created` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
