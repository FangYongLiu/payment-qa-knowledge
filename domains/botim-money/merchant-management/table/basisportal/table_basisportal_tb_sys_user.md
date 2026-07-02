---
id: tbl_basisportal_tb_sys_user
object_type: Table
name: user table (tb_sys_user)
aliases: [tb_sys_user, basisportal.tb_sys_user]
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

# user table (tb_sys_user)

## 用途
物理表 `basisportal.tb_sys_user`,主键 `user_id`。user table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `user_id` | bigint | primary key |
| `avatar` | varchar(128) | avatar · 可空 |
| `account` | varchar(45) | account · 可空 |
| `password` | varchar(45) | password · 可空 |
| `salt` | varchar(45) | md5 password salt · 可空 |
| `name` | varchar(45) | name · 可空 |
| `birthday` | timestamp | birthday · 可空 |
| `sex` | char | gender (dictionary) · 可空 |
| `email` | varchar(45) | email · 可空 |
| `phone` | varchar(45) | phone · 可空 |
| `role_id` | varchar(255) | role id (comma separated) · 可空 |
| `dept_id` | bigint | department id (comma separated) · 可空 |
| `status` | varchar(32) | status (dictionary) · 可空 |
| `create_time` | timestamp | creation time · 可空 |
| `create_user` | bigint | creator · 可空 |
| `update_time` | timestamp | update time · 可空 |
| `update_user` | bigint | updater · 可空 |
| `version` | int | version · 可空 |

## 主键 / 索引
- 主键:`user_id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
