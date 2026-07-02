---
id: tbl_officer_sys_user
object_type: Table
name: system user (sys_user)
aliases: [sys_user, officer.sys_user]
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

# system user (sys_user)

## 用途
物理表 `officer.sys_user`,主键 `user_id`。system user。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `user_id` | bigint | ID · 可空 |
| `dept_id` | bigint | Department Name · 可空 |
| `username` | varchar(255) | Username · 可空 |
| `nick_name` | varchar(255) | Nickname · 可空 |
| `gender` | varchar(6) | Gender · 可空 |
| `phone` | varchar(100) | Mobile phone number · 可空 |
| `email` | varchar(255) | Email · 可空 |
| `avatar_name` | varchar(255) | Avatar address · 可空 |
| `avatar_path` | varchar(255) | Avatar real path · 可空 |
| `password` | varchar(255) | Password · 可空 |
| `is_admin` | tinyint | Is it an admin account? · 可空 |
| `enabled` | tinyint | Status: 1 enabled, 0 disabled · 可空 |
| `create_by` | varchar(100) | creator · 可空 |
| `update_by` | varchar(100) | 更新着 · 可空 |
| `pwd_reset_time` | timestamp | Time to change the password · 可空 |
| `create_time` | timestamp | Creation date · 可空 |
| `update_time` | timestamp | Update time · 可空 |
| `uid` | varchar(100) | uid · 可空 |
| `ldap_username` | varchar(64) | Internal users username in ldap · 可空 |
| `is_new` | tinyint | Is it a new employee? 0 Old employee 1 New employee · 可空 |
| `is_help` | tinyint | Whether to assist 0 Fixed 1 assist · 可空 |

## 主键 / 索引
- 主键:`user_id`
- `uk_uniq_email`:email (UNIQUE)
- `uk_uniq_username`:username (UNIQUE)
- `idx_avatar`:avatar_name
- `idx_deptId_uid`:dept_id, uid
- `idx_uid`:uid

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
