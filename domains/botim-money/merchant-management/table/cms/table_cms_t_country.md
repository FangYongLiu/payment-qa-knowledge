---
id: tbl_cms_t_country
object_type: Table
name: 国家表 (t_country)
aliases: [t_country, cms.t_country]
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

# 国家表 (t_country)

## 用途
物理表 `cms.t_country`,主键 `id`。国家表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(17) | 待补 |
| `country_code` | varchar(8) | 国家Code |
| `country_full_name` | varchar(64) | 国家全称 |
| `country_simple_name` | varchar(32) | 国家简称 |
| `english_name` | varchar(32) | 英文名称 |
| `icon` | varchar(255) | 国家icon地址 |
| `status` | tinyint | 数据状态 1:有效 0:无效 |
| `create_user` | bigint | 创建人 |
| `modify_user` | bigint | 修改人 · 可空 |
| `gmt_created` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
