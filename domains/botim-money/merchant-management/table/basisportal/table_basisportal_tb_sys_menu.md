---
id: tbl_basisportal_tb_sys_menu
object_type: Table
name: menu table (tb_sys_menu)
aliases: [tb_sys_menu, basisportal.tb_sys_menu]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: basisportal schema DDL
tags: [merchant-management, basisportal]
sensitivity: normal
related_services: []
---

# menu table (tb_sys_menu)

## 用途
物理表 `basisportal.tb_sys_menu`,主键 `menu_id`。menu table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `menu_id` | bigint | primary key |
| `code` | varchar(64) | menu code · 可空 |
| `pcode` | varchar(64) | parent menu code · 可空 |
| `pcodes` | varchar(255) | all parent menu codes · 可空 |
| `name` | varchar(64) | menu name · 可空 |
| `icon` | varchar(64) | menu icon · 可空 |
| `url` | varchar(128) | url · 可空 |
| `sort` | int(8) | menu sort order · 可空 |
| `levels` | int(8) | menu level · 可空 |
| `menu_flag` | char | is menu (dictionary) · 可空 |
| `description` | varchar(128) | remark · 可空 |
| `status` | varchar(16) | menu status (dictionary) · 可空 |
| `new_page_flag` | varchar(32) | is open new page (dictionary) · 可空 |
| `open_flag` | char | is open (dictionary) · 可空 |
| `create_time` | timestamp | creation time · 可空 |
| `update_time` | timestamp | update time · 可空 |
| `create_user` | bigint | creator · 可空 |
| `update_user` | bigint | updater · 可空 |
| `is_sensitive` | char | is sensitive Y:Yes N:No · 可空 |

## 主键 / 索引
- 主键:`menu_id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
