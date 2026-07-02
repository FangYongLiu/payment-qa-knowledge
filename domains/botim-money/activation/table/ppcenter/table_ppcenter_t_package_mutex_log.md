---
id: tbl_ppcenter_t_package_mutex_log
object_type: Table
name: product mutex config-change audit log (t_package_mutex_log)
aliases: [t_package_mutex_log, ppcenter.t_package_mutex_log]
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ppcenter schema DDL
tags: [activation, ppcenter]
sensitivity: normal
related_services: []
---

# product mutex config-change audit log (t_package_mutex_log)

## 用途
物理表 `ppcenter.t_package_mutex_log`,主键 `id`。product mutex config-change audit log。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint unsigned | PK · 可空 |
| `group_id` | bigint | FK to t_package_mutex_group_define.id |
| `package_code` | varchar(64) | affected package; NULL for group-level changes · 可空 |
| `action` | varchar(32) | ADD_ITEM/REMOVE_ITEM/ITEM_ENABLE/ITEM_DISABLE/GROUP_CREATE/GROUP_UPDATE/GROUP_ENABLE/GROUP_DISABLE |
| `memo` | varchar(128) | operator-supplied reason · 可空 |
| `operator` | varchar(64) | configurator from Basis |
| `gmt_create` | timestamp | create time |
| `gmt_modify` | timestamp | mapping-change time |
| `mutex_created` | timestamp | Store the create time directly from mutex define table |

## 主键 / 索引
- 主键:`id`
- `idx_log_group_id`:group_id
- `idx_log_package_code`:package_code

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
