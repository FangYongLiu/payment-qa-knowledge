---
id: tbl_cms_t_store_category
object_type: Table
name: t_store_category (t_store_category)
aliases: [t_store_category, cms.t_store_category]
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

# t_store_category (t_store_category)

## 用途
物理表 `cms.t_store_category`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(17) | 待补 |
| `category` | varchar(20) | 类别 |
| `category_desc` | varchar(50) | 描述 |
| `icon` | varchar(150) | icon地址 |
| `status` | tinyint | 状态 1：开启 0：关闭 |
| `gmt_created` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改时间 |
| `create_user` | bigint | 创建用户 · 可空 |
| `modify_user` | bigint | 修改用户 · 可空 |
| `default_icon` | varchar(150) | 类别默认icon |
| `active_icon` | varchar(150) | 激活icon |
| `seq` | int | 顺序 |

## 主键 / 索引
- 主键:`id`
- `uk_store_category`:category (UNIQUE)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
