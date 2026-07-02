---
id: tbl_credit_t_cs_grant_consent_record
object_type: Table
name: grant consent record (t_cs_grant_consent_record)
aliases: [t_cs_grant_consent_record, credit.t_cs_grant_consent_record]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: credit schema DDL
tags: [lending, credit]
sensitivity: normal
related_services: []
---

# grant consent record (t_cs_grant_consent_record)

## 用途
物理表 `credit.t_cs_grant_consent_record`,主键 `id`。grant consent record。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int(11) | id · 可空 |
| `created_time` | timestamp | create time |
| `user_id` | varchar(20) | user member id |
| `scene` | varchar(30) | grant scene |
| `type` | varchar(30) | consent type |
| `flag` | tinyint(5) | 0false 1true |
| `consent_time` | timestamp | consent time |

## 主键 / 索引
- 主键:`id`
- `idx_created_time`:created_time
- `idx_user_id`:user_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
