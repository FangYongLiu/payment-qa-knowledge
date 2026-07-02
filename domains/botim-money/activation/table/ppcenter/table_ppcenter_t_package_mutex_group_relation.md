---
id: tbl_ppcenter_t_package_mutex_group_relation
object_type: Table
name: product mutex group membership (group<->package) (t_package_mutex_group_relation)
aliases: [t_package_mutex_group_relation, ppcenter.t_package_mutex_group_relation]
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

# product mutex group membership (group<->package) (t_package_mutex_group_relation)

## 用途
物理表 `ppcenter.t_package_mutex_group_relation`,主键 `id`。product mutex group membership (group<->package)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint unsigned | PK · 可空 |
| `group_id` | bigint | FK to t_package_mutex_group_define.id |
| `package_code` | varchar(64) | package_code (t_product_package) |
| `status` | tinyint(1) | enabled=1 and disabled=0 |
| `gmt_create` | timestamp | create time |
| `gmt_modify` | timestamp | modify time |

## 主键 / 索引
- 主键:`id`
- `uniq_group_package`:group_id, package_code (UNIQUE)
- `idx_package_code`:package_code

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
