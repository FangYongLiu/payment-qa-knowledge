---
id: tbl_basis_tb_sys_user
object_type: Table
name: 管理员表 (tb_sys_user)
aliases: [tb_sys_user, basis.tb_sys_user]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: basis schema DDL
tags: [merchant-management, basis]
sensitivity: normal
related_services: []
---

# 管理员表 (tb_sys_user)

## 用途
物理表 `basis.tb_sys_user`,主键 `user_id`。管理员表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `user_id` | bigint | 主键id |
| `avatar` | varchar(255) | 头像 · 可空 |
| `account` | varchar(45) | 账号 · 可空 |
| `password` | varchar(45) | 密码 · 可空 |
| `salt` | varchar(45) | md5密码盐 · 可空 |
| `name` | varchar(45) | 名字 · 可空 |
| `birthday` | timestamp | 生日 · 可空 |
| `sex` | varchar(32) | 性别(字典) · 可空 |
| `email` | varchar(45) | 电子邮件 · 可空 |
| `phone` | varchar(45) | 电话 · 可空 |
| `role_id` | varchar(255) | 角色id(多个逗号隔开) · 可空 |
| `dept_id` | bigint | 部门id(多个逗号隔开) · 可空 |
| `status` | varchar(32) | 状态(字典) · 可空 |
| `create_time` | timestamp | 创建时间 · 可空 |
| `create_user` | bigint | 创建人 · 可空 |
| `update_time` | timestamp | 更新时间 · 可空 |
| `update_user` | bigint | 更新人 · 可空 |
| `version` | int | 乐观锁 · 可空 |

## 主键 / 索引
- 主键:`user_id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
