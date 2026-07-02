---
id: tbl_cms_t_config_template
object_type: Table
name: 配置模版表 (t_config_template)
aliases: [t_config_template, cms.t_config_template]
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

# 配置模版表 (t_config_template)

## 用途
物理表 `cms.t_config_template`,主键 `id`。配置模版表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 待补 · 可空 |
| `type` | varchar(50) | 类型 |
| `name` | varchar(50) | 名称 |
| `memo` | varchar(255) | 备注 · 可空 |
| `preview_img` | varchar(128) | 预览图 · 可空 |
| `gmt_created` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`id`
- `uk_type`:type (UNIQUE)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
