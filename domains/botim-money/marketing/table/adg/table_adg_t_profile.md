---
id: tbl_adg_t_profile
object_type: Table
name: User profile information (t_profile)
aliases: [t_profile, adg.t_profile]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: adg schema DDL
tags: [marketing, adg]
sensitivity: normal
related_services: []
---

# User profile information (t_profile)

## 用途
物理表 `adg.t_profile`,主键 `id`。User profile information。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Unique identifier, primary key · 可空 |
| `user_id` | varchar(63) | Unique user identifier, primary key |
| `eid` | varchar(63) | Emirates ID number · 可空 |
| `eid_expiry_date` | date | Emirates ID expiry date · 可空 |
| `email` | varchar(127) | User email address · 可空 |
| `full_name` | varchar(511) | User full name · 可空 |
| `mobile` | varchar(31) | User mobile number · 可空 |
| `create_at` | timestamp | Record creation timestamp |
| `updated_at` | timestamp | Record last update timestamp |
| `trade_license_number` | varchar(50) | Trade license number · 可空 |
| `issuing_authority` | varchar(50) | Authority issuing the license (e.g. DED-DUBAI, JAFZA) · 可空 |

## 主键 / 索引
- 主键:`id`
- `uk_user_id`:user_id (UNIQUE)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
