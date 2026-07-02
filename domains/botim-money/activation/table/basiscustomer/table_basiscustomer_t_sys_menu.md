---
id: tbl_basiscustomer_t_sys_menu
object_type: Table
name: 菜单表 (t_sys_menu)
aliases: [t_sys_menu, basiscustomer.t_sys_menu]
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: basiscustomer schema DDL
tags: [activation, basiscustomer]
sensitivity: normal
related_services: []
---

# 菜单表 (t_sys_menu)

## 用途
物理表 `basiscustomer.t_sys_menu`,主键 `menu_id`。菜单表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `menu_id` | bigint | 主键id · 可空 |
| `code` | varchar(128) | 菜单编号 · 可空 |
| `pcode` | varchar(255) | 菜单父编号 · 可空 |
| `pcodes` | varchar(255) | 当前菜单的所有父菜单编号 · 可空 |
| `name` | varchar(255) | 菜单名称 · 可空 |
| `icon` | varchar(255) | 菜单图标 · 可空 |
| `url` | varchar(255) | url地址 · 可空 |
| `sort` | int(65) | 菜单排序号 · 可空 |
| `levels` | int(65) | 菜单层级 · 可空 |
| `menu_flag` | char | 是否是菜单(字典) · 可空 |
| `description` | varchar(255) | 备注 · 可空 |
| `status` | varchar(32) | 菜单状态(字典) · 可空 |
| `new_page_flag` | varchar(32) | 是否打开新页面的标识(字典) · 可空 |
| `open_flag` | varchar(32) | 是否打开(字典) · 可空 |
| `create_time` | timestamp | 创建时间 · 可空 |
| `update_time` | timestamp | 修改时间 · 可空 |
| `create_user` | bigint | 创建人 · 可空 |
| `update_user` | bigint | 修改人 · 可空 |
| `is_sensitive` | char | 是否敏感 Y:是 N:否 · 可空 |

## 主键 / 索引
- 主键:`menu_id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
