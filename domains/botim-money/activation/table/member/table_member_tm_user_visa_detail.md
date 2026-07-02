---
id: tbl_member_tm_user_visa_detail
object_type: Table
name: Active Visa (tm_user_visa_detail)
aliases: [tm_user_visa_detail, member.tm_user_visa_detail]
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: member schema DDL
tags: [activation, member]
sensitivity: normal
related_services: []
---

# Active Visa (tm_user_visa_detail)

## 用途
物理表 `member.tm_user_visa_detail`,主键 `id`。Active Visa。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint unsigned | Primary Key · 可空 |
| `entity_id` | bigint | Entity ID |
| `visa_type` | varchar(50) | Visa category: Work, Visit, Residence, Transit, Student, Mission · 可空 |
| `visa_department` | varchar(200) | Government department that issued the visa · 可空 |
| `passport_no` | varchar(20) | Passport number linked to this visa · 可空 |
| `passport_expiry_date` | varchar(10) | Expiry date of the linked passport (YYYY-MM-DD) · 可空 |
| `passport_issue_place` | varchar(100) | City or country where the linked passport was issued · 可空 |
| `visa_status` | varchar(50) | Current visa status: USED, CLOSED, CANCELLED, CHANGE STATUS, EXTENDED, VIOLATED · 可空 |
| `issue_date` | varchar(10) | Visa issue date (YYYY-MM-DD) · 可空 |
| `created_date` | varchar(10) | Date the visa record was created (YYYY-MM-DD) · 可空 |
| `validity_date` | varchar(10) | Date until which the visa is valid for entry (YYYY-MM-DD) · 可空 |
| `expiry_date` | varchar(10) | Visa expiry date (YYYY-MM-DD) · 可空 |
| `source` | varchar(50) | Source · 可空 |
| `extension` | varchar(255) | Extension · 可空 |
| `create_time` | timestamp | Create Time |
| `update_time` | timestamp | Update Time |

## 主键 / 索引
- 主键:`id`
- `idx_entity_id`:entity_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
