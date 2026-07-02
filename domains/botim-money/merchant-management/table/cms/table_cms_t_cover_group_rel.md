---
id: tbl_cms_t_cover_group_rel
object_type: Table
name: 模版表 (t_cover_group_rel)
aliases: [t_cover_group_rel, cms.t_cover_group_rel]
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

# 模版表 (t_cover_group_rel)

## 用途
物理表 `cms.t_cover_group_rel`,主键 `id`。模版表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(17) | 主键 |
| `group_id` | bigint(17) | 封面组ID |
| `cover_id` | bigint(17) | 封面ID |
| `seq` | int | 顺序 · 可空 |
| `gmt_created` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
