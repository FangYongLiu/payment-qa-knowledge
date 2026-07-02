---
id: tbl_collection_sys_menu
object_type: Table
name: 系统菜单 (sys_menu)
aliases: [sys_menu, collection.sys_menu]
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: collection schema DDL
tags: [risk, collection]
sensitivity: normal
related_services: []
---

# 系统菜单 (sys_menu)

## 用途
物理表 `collection.sys_menu`,主键 `menu_id`。系统菜单。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `menu_id` | bigint | ID · 可空 |
| `pid` | bigint | 上级菜单ID · 可空 |
| `sub_count` | int(5) | 子菜单数目 · 可空 |
| `type` | tinyint(5) | 菜单类型 · 可空 |
| `title` | varchar(200) | 菜单标题 · 可空 |
| `name` | varchar(255) | 组件名称 · 可空 |
| `component` | varchar(255) | 组件 · 可空 |
| `menu_sort` | int(5) | 排序 · 可空 |
| `icon` | varchar(255) | 图标 · 可空 |
| `path` | varchar(255) | 链接地址 · 可空 |
| `i_frame` | tinyint(5) | 是否外链 · 可空 |
| `cache` | tinyint(2) | 缓存 · 可空 |
| `hidden` | tinyint(2) | 隐藏 · 可空 |
| `permission` | varchar(100) | 权限 · 可空 |
| `create_by` | varchar(100) | 创建者 · 可空 |
| `update_by` | varchar(100) | 更新者 · 可空 |
| `create_time` | timestamp | 创建日期 · 可空 |
| `update_time` | timestamp | 更新时间 · 可空 |

## 主键 / 索引
- 主键:`menu_id`
- `uk_uniq_name`:name (UNIQUE)
- `uk_uniq_title`:title (UNIQUE)
- `inx_pid`:pid

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
