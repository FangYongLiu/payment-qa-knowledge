---
id: tbl_collection_sys_user
object_type: Table
name: 系统用户 (sys_user)
aliases: [sys_user, collection.sys_user]
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: collection schema DDL
tags: [risk, collection]
sensitivity: normal
related_services: []
---

# 系统用户 (sys_user)

## 用途
物理表 `collection.sys_user`,主键 `user_id`。系统用户。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `user_id` | bigint | ID · 可空 |
| `dept_id` | bigint | 部门名称 · 可空 |
| `username` | varchar(255) | 用户名 · 可空 |
| `nick_name` | varchar(255) | 昵称 · 可空 |
| `gender` | varchar(2) | 性别 · 可空 |
| `phone` | varchar(100) | 手机号码 · 可空 |
| `email` | varchar(255) | 邮箱 · 可空 |
| `avatar_name` | varchar(255) | 头像地址 · 可空 |
| `avatar_path` | varchar(255) | 头像真实路径 · 可空 |
| `password` | varchar(255) | 密码 · 可空 |
| `is_admin` | tinyint(5) | 是否为admin账号 · 可空 |
| `enabled` | tinyint(2) | 状态：1启用、0禁用 · 可空 |
| `create_by` | varchar(100) | 创建者 · 可空 |
| `update_by` | varchar(100) | 更新着 · 可空 |
| `pwd_reset_time` | timestamp | 修改密码的时间 · 可空 |
| `create_time` | timestamp | 创建日期 · 可空 |
| `update_time` | timestamp | 更新时间 · 可空 |
| `uid` | varchar(100) | uid · 可空 |
| `ldap_username` | varchar(64) | 内部用户在ldap的用户名 · 可空 |
| `is_new` | tinyint(2) | 是否新员工 0 老员工 1新员工 · 可空 |
| `is_help` | tinyint(2) | 是否协催 0 固定 1协催 · 可空 |
| `third_party_token` | varchar(255) | Third party login token · 可空 |

## 主键 / 索引
- 主键:`user_id`
- `uk_uniq_email`:email (UNIQUE)
- `uk_uniq_username`:username (UNIQUE)
- `idx_avatar`:avatar_name
- `idx_dept`:dept_id
- `idx_uid`:uid

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
