---
id: tbl_cfca_menu
object_type: Table
name: menu (menu)
aliases: [menu, cfca.menu]
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: cfca schema DDL
tags: [activation, cfca]
sensitivity: normal
related_services: []
---

# menu (menu)

## 用途
物理表 `cfca.menu`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(10) | 待补 · 可空 |
| `alias` | varchar(255) | 待补 · 可空 |
| `create_time` | datetime | 待补 · 可空 |
| `icon` | varchar(255) | 待补 · 可空 |
| `name` | varchar(255) | 待补 |
| `remark` | varchar(255) | 待补 · 可空 |
| `sequence` | bigint(11) | 待补 · 可空 |
| `status` | bigint(1) | 待补 · 可空 |
| `target` | varchar(255) | 待补 · 可空 |
| `url` | varchar(255) | 待补 · 可空 |
| `parent_id` | bigint(11) | 待补 · 可空 |
| `foreign` | key | 待补 · 可空 |

## 主键 / 索引
- 主键:`id`
- `IDX_MENU_PARENT_ID`:parent_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
