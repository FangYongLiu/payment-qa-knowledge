---
id: tbl_installmentcard_t_ic_am_profile
object_type: Table
name: Table will have the user's detail (t_ic_am_profile)
aliases: [t_ic_am_profile, installmentcard.t_ic_am_profile]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: installmentcard schema DDL
tags: [lending, installmentcard]
sensitivity: normal
related_services: []
---

# Table will have the user's detail (t_ic_am_profile)

## 用途
物理表 `installmentcard.t_ic_am_profile`,主键 `member_id`。Table will have the user's detail。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `member_id` | varchar(20) | payby id for the user also primary key |
| `mobile_no` | varchar(32) | user's mobile number |
| `email_address` | varchar(255) | email · 可空 |
| `gender` | varchar(20) | Gender of the user: MALE, FEMALE, NOT_SPECIFIED, OTHER · 可空 |
| `birthday` | date | user's date of birth · 可空 |
| `name` | varchar(200) | user's name · 可空 |
| `passport_no` | varchar(50) | user's passport number · 可空 |
| `nationality` | varchar(64) | nationality of user · 可空 |
| `emirates_id` | varchar(50) | user's emirates id · 可空 |
| `eid_issue_place` | varchar(64) | Emirates ID issue place/location · 可空 |
| `eid_expiry` | date | Expiration time of user identity document · 可空 |
| `user_status` | varchar(20) | User status: ACTIVE, INACTIVE, EXPIRED, HOLD |
| `create_time` | timestamp | record create time |
| `last_modified` | timestamp | record last updated time |

## 主键 / 索引
- 主键:`member_id`
- `idx_user_profile_mobile_no`:mobile_no

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
