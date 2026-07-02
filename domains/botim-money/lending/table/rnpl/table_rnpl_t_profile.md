---
id: tbl_rnpl_t_profile
object_type: Table
name: User Information Table (t_profile)
aliases: [t_profile, rnpl.t_profile]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: rnpl schema DDL
tags: [lending, rnpl]
sensitivity: normal
related_services: []
---

# User Information Table (t_profile)

## 用途
物理表 `rnpl.t_profile`,主键 `id`。User Information Table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | primary key · 可空 |
| `mobile` | varchar(32) | mobile number |
| `user_id` | varchar(20) | user ID |
| `sex` | tinyint | sex · 可空 |
| `birthday` | varchar(10) | birthday · 可空 |
| `name` | varchar(200) | name · 可空 |
| `identity` | varchar(50) | identification card · 可空 |
| `identity_invalid_time` | varchar(10) | expiration time · 可空 |
| `passport_no` | varchar(50) | passport number · 可空 |
| `nationality` | varchar(64) | nationality · 可空 |
| `create_time` | timestamp | create time |
| `last_modified` | timestamp | update time |
| `email_address` | varchar(255) | email · 可空 |

## 主键 / 索引
- 主键:`id`
- `uk_user_id`:user_id (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
