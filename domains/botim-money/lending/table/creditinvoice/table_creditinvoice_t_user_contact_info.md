---
id: tbl_creditinvoice_t_user_contact_info
object_type: Table
name: User contact info + KYC cache (t_user_contact_info)
aliases: [t_user_contact_info, creditinvoice.t_user_contact_info]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: creditinvoice schema DDL
tags: [lending, creditinvoice]
sensitivity: normal
related_services: []
---

# User contact info + KYC cache (t_user_contact_info)

## 用途
物理表 `creditinvoice.t_user_contact_info`,主键 `id`。User contact info + KYC cache。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint unsigned | Primary key · 可空 |
| `member_id` | varchar(20) | PayBy memberId |
| `phone` | varchar(20) | Phone number in plain text (with country code +971) |
| `verified_email` | varchar(128) | Verified email · 可空 |
| `eid` | varchar(64) | KYC EID cache (credit-UES ticket) · 可空 |
| `full_name` | varchar(128) | KYC full name cache (credit-UES ticket) · 可空 |
| `kyc_expire_time` | timestamp | KYC expiry time, taken from PayBy invalidTime · 可空 |
| `create_time` | timestamp | create time |
| `update_time` | timestamp | update time |

## 主键 / 索引
- 主键:`id`
- `uk_member_id`:member_id (UNIQUE)
- `idx_phone`:phone

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
