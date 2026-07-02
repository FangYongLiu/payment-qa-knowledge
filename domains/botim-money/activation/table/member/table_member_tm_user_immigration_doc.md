---
id: tbl_member_tm_user_immigration_doc
object_type: Table
name: Immigration and Documents (tm_user_immigration_doc)
aliases: [tm_user_immigration_doc, member.tm_user_immigration_doc]
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

# Immigration and Documents (tm_user_immigration_doc)

## 用途
物理表 `member.tm_user_immigration_doc`,主键 `id`。Immigration and Documents。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key · 可空 |
| `entity_id` | bigint | Entity ID |
| `status` | varchar(50) | Status · 可空 |
| `issue_date` | date | Issue Date · 可空 |
| `issue_place` | varchar(255) | Issue Place · 可空 |
| `expiry_date` | datetime | Expiry Date · 可空 |
| `file_number` | varchar(100) | File Number · 可空 |
| `file_type_ar` | varchar(100) | File Type Ar · 可空 |
| `file_type_en` | varchar(100) | File Type En · 可空 |
| `digital_signature` | varchar(100) | Digital Signature Tag · 可空 |
| `digital_eid` | varchar(100) | Digital EID Tag · 可空 |
| `person_face` | varchar(100) | Person Face Tag · 可空 |
| `certificate` | varchar(100) | Certificate Tag · 可空 |
| `uid_num` | varchar(85) | Uid Number · 可空 |
| `source_id` | varchar(85) | Channel source id, eg: uaeKycId · 可空 |
| `source` | varchar(50) | Source · 可空 |
| `extension` | varchar(255) | Extension · 可空 |
| `create_time` | timestamp | Create Time |
| `update_time` | timestamp | Update Time |

## 主键 / 索引
- 主键:`id`
- `idx_entity_id`:entity_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
