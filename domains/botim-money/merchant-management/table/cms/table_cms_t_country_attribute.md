---
id: tbl_cms_t_country_attribute
object_type: Table
name: 国家属性表 (t_country_attribute)
aliases: [t_country_attribute, cms.t_country_attribute]
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

# 国家属性表 (t_country_attribute)

## 用途
物理表 `cms.t_country_attribute`,主键 `id`。国家属性表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(17) | 待补 |
| `country_id` | bigint(17) | 国家ID |
| `area_code` | varchar(10) | 国家区号 |
| `phone_regex` | varchar(64) | 国家手机正则 · 可空 |
| `gmt_created` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改时间 · 可空 |
| `is_open_reg` | tinyint | 是否开放注册 1:开放 0:不开放 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
