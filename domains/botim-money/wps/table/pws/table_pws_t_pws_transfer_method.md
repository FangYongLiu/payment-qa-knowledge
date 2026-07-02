---
id: tbl_pws_t_pws_transfer_method
object_type: Table
name: pws transfer method (t_pws_transfer_method)
aliases: [t_pws_transfer_method, pws.t_pws_transfer_method]
domain: wps
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: pws schema DDL
tags: [wps, pws]
sensitivity: normal
related_services: []
---

# pws transfer method (t_pws_transfer_method)

## 用途
物理表 `pws.t_pws_transfer_method`,主键 `id`。pws transfer method。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | varchar(32) | ulid |
| `scene` | varchar(32) | scene |
| `description` | varchar(127) | description |
| `name` | varchar(127) | name |
| `method_type` | varchar(30) | method type |
| `limit_verify` | tinyint | limit verify  |
| `enable` | tinyint | enable |
| `is_available` | tinyint | is available · 可空 |
| `is_deleted` | tinyint | is deleted · 可空 |
| `create_at` | timestamp | created time |
| `update_at` | timestamp | updated time |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
