---
id: tbl_collection_col_debtor
object_type: Table
name: 债务人 (col_debtor)
aliases: [col_debtor, collection.col_debtor]
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

# 债务人 (col_debtor)

## 用途
物理表 `collection.col_debtor`,主键 `id`。债务人。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主健 · 可空 |
| `create_by` | varchar(255) | 创建者 · 可空 |
| `create_time` | timestamp | 创建时间 · 可空 |
| `update_time` | timestamp | 更新时间 · 可空 |
| `update_by` | varchar(100) | 更新人员 · 可空 |
| `birthday` | varchar(20) | 生日 · 可空 |
| `email` | varchar(255) | 邮箱 · 可空 |
| `emergency_contct` | varchar(500) | 紧急联系人 · 可空 |
| `identity` | varchar(100) | 身份证 |
| `member_id` | varchar(20) | id |
| `name` | varchar(255) | 名称 |
| `nationality` | varchar(100) | 国籍 · 可空 |
| `phone` | varchar(128) | 手机号 · 可空 |
| `sex` | tinyint(5) | 性别 |
| `status` | tinyint(5) | 状态 初始0正常 |
| `occupation` | varchar(100) | 职业 · 可空 |
| `address` | varchar(255) | 地址 · 可空 |
| `identity_invalid_time` | timestamp | 身份证过期时间 · 可空 |
| `white_list_user` | tinyint(5) | 是否白名单 |
| `passport_no` | varchar(50) | 护照 · 可空 |
| `salary_date` | varchar(64) | 用户填写的发薪日 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_identity`:identity
- `idx_member_id`:member_id
- `idx_phone`:phone

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
