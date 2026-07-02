---
id: tbl_atbeb_t_lock
object_type: Table
name: should acquire retry lock before scanning t_event (t_lock)
aliases: [t_lock, atbeb.t_lock]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: atbeb schema DDL
tags: [marketing, atbeb]
sensitivity: normal
related_services: []
---

# should acquire retry lock before scanning t_event (t_lock)

## 用途
物理表 `atbeb.t_lock`,主键 `id`。should acquire retry lock before scanning t_event。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Auto-incrementing primary key · 可空 |
| `lock_name` | varchar(20) | lock name |
| `locked_by` | varchar(64) | locked by which server |
| `lock_at` | bigint | lock time, milliseconds |
| `expire_at` | bigint | lock expire time, milliseconds |
| `status` | tinyint | Status, 0-unlocked, 1-locked |
| `create_at` | datetime | Create timestamp |
| `update_at` | datetime | Update timestamp |

## 主键 / 索引
- 主键:`id`
- `uniq_lock_name`:lock_name (UNIQUE)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
