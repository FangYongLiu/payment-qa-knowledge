---
id: tbl_afis_t_infra_conf
object_type: Table
name: configuration items in database (t_infra_conf)
aliases: [t_infra_conf, afis.t_infra_conf]
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: afis schema DDL
tags: [risk, afis]
sensitivity: normal
related_services: []
---

# configuration items in database (t_infra_conf)

## 用途
物理表 `afis.t_infra_conf`,主键 `id`。configuration items in database。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | ulid |
| `name_space` | varchar(255) | namespace of the configuration |
| `name_key` | varchar(255) | key of the configuration |
| `value` | varchar(2048) | value of the configuration in |
| `description` | varchar(1024) | description of the configuration · 可空 |
| `create_at` | timestamp | create time |
| `update_at` | timestamp | update time |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
