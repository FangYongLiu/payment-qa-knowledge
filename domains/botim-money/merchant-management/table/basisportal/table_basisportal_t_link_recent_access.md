---
id: tbl_basisportal_t_link_recent_access
object_type: Table
name: recent access link table (t_link_recent_access)
aliases: [t_link_recent_access, basisportal.t_link_recent_access]
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

# recent access link table (t_link_recent_access)

## 用途
物理表 `basisportal.t_link_recent_access`,主键 `id`。recent access link table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(21) | primary key |
| `sub_system` | varchar(32) | subsystem name · 可空 |
| `url` | varchar(128) | URL of the recent access link · 可空 |
| `menu_id` | bigint(21) | menu id · 可空 |
| `menu_name` | varchar(64) | menu name · 可空 |
| `p_menu_path` | varchar(255) | parent menu path · 可空 |
| `create_by` | bigint(21) | creator · 可空 |
| `create_time` | timestamp | creation time · 可空 |
| `update_time` | timestamp | update time · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
