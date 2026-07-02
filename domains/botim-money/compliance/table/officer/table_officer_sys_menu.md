---
id: tbl_officer_sys_menu
object_type: Table
name: System menu (sys_menu)
aliases: [sys_menu, officer.sys_menu]
domain: compliance
status: active
owner: dewen.li
reviewer: dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: officer schema DDL
tags: [compliance, officer]
sensitivity: normal
related_services: []
---

# System menu (sys_menu)

## 用途
物理表 `officer.sys_menu`,主键 `menu_id`。System menu。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `menu_id` | bigint | ID · 可空 |
| `pid` | bigint | Previous menu ID · 可空 |
| `sub_count` | int | Number of submenus · 可空 |
| `type` | tinyint | Menu type · 可空 |
| `title` | varchar(200) | Menu title · 可空 |
| `name` | varchar(255) | Component name · 可空 |
| `component` | varchar(255) | component · 可空 |
| `menu_sort` | int | Sort · 可空 |
| `icon` | varchar(255) | icon · 可空 |
| `path` | varchar(255) | Link address · 可空 |
| `i_frame` | tinyint | Is it an external link? · 可空 |
| `cache` | tinyint | cache · 可空 |
| `hidden` | tinyint | Hidden · 可空 |
| `permission` | varchar(100) | Permission · 可空 |
| `create_by` | varchar(100) | creator · 可空 |
| `update_by` | varchar(100) | Updater · 可空 |
| `create_time` | timestamp | Creation date · 可空 |
| `update_time` | timestamp | Update time · 可空 |

## 主键 / 索引
- 主键:`menu_id`
- `uk_uniq_name`:name (UNIQUE)
- `uk_uniq_title`:title (UNIQUE)
- `inx_pid`:pid

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
