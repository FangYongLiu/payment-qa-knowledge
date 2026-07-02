---
id: tbl_cms_t_cover_param
object_type: Table
name: 封面图片表 (t_cover_param)
aliases: [t_cover_param, cms.t_cover_param]
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

# 封面图片表 (t_cover_param)

## 用途
物理表 `cms.t_cover_param`,主键 `id`。封面图片表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(17) | 主键 |
| `cover_id` | bigint(17) | 封面ID |
| `type` | varchar(100) | 类型 |
| `key_code` | varchar(100) | 封面Key |
| `value` | varchar(300) | URL |
| `gmt_created` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改时间 |
| `create_user` | bigint | 创建用户 · 可空 |
| `modify_user` | bigint | 修改用户 · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
