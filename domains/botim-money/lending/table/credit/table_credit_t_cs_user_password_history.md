---
id: tbl_credit_t_cs_user_password_history
object_type: Table
name: user password change history (t_cs_user_password_history)
aliases: [t_cs_user_password_history, credit.t_cs_user_password_history]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: credit schema DDL
tags: [lending, credit]
sensitivity: normal
related_services: []
---

# user password change history (t_cs_user_password_history)

## 用途
物理表 `credit.t_cs_user_password_history`,主键 `id`。user password change history。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int(11) | id · 可空 |
| `user_id` | varchar(20) | user ID |
| `password` | varchar(64) | password after sha256 |
| `created_at` | timestamp | created time |

## 主键 / 索引
- 主键:`id`
- `idx_user_id`:user_id

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
