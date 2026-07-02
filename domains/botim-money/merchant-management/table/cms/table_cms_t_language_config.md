---
id: tbl_cms_t_language_config
object_type: Table
name: 语言方案表 (t_language_config)
aliases: [t_language_config, cms.t_language_config]
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

# 语言方案表 (t_language_config)

## 用途
物理表 `cms.t_language_config`,主键 `config_id`。语言方案表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `config_id` | bigint(18) | 主键 · 可空 |
| `lang_type` | varchar(8) | 语言 |
| `placeholder` | varchar(50) | 占位符 |
| `client_id` | varchar(50) | 客户端:page,section,item |
| `lang_text` | varchar(200) | 语言文本 |
| `gmt_used` | datetime | 使用时间 · 可空 |
| `memo` | varchar(200) | 备注 · 可空 |
| `gmt_created` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`config_id`
- `t_language_config_pk`:placeholder, lang_type (UNIQUE)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
