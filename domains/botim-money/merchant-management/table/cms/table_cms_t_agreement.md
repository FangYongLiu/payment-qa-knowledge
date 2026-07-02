---
id: tbl_cms_t_agreement
object_type: Table
name: 协议表 (t_agreement)
aliases: [t_agreement, cms.t_agreement]
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

# 协议表 (t_agreement)

## 用途
物理表 `cms.t_agreement`,主键 `agreement_id`。协议表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `agreement_id` | bigint(18) | 协议id |
| `name` | varchar(200) | 协议名称 |
| `type` | varchar(32) | 协议类型 |
| `version` | varchar(10) | 协议版本号 |
| `language` | varchar(10) | 协议语言 |
| `text_status` | varchar(10) | 文稿状态 |
| `url` | varchar(500) | 协议链接 · 可空 |
| `agreement_status` | varchar(10) | 协议状态 |
| `create_date` | timestamp | 创建时间 · 可空 |
| `create_user` | varchar(32) | 创建人 · 可空 |
| `update_date` | timestamp | 修改时间 · 可空 |
| `update_user` | varchar(32) | 修改人 · 可空 |
| `memo` | varchar(225) | 待补 · 可空 |

## 主键 / 索引
- 主键:`agreement_id`
- `uk_index_agreement`:name, type, version, language (UNIQUE)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
