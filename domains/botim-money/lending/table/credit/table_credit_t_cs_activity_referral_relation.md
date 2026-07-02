---
id: tbl_credit_t_cs_activity_referral_relation
object_type: Table
name: Referral relationship record table (t_cs_activity_referral_relation)
aliases: [t_cs_activity_referral_relation, credit.t_cs_activity_referral_relation]
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

# Referral relationship record table (t_cs_activity_referral_relation)

## 用途
物理表 `credit.t_cs_activity_referral_relation`,主键 `id`。Referral relationship record table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | Primary key · 可空 |
| `referrer_user_id` | varchar(20) | Referrer user ID |
| `referee_user_id` | varchar(20) | Referee user ID |
| `referral_code` | varchar(6) | Referral code |
| `created_time` | timestamp | Binding time |
| `expired_time` | timestamp | Expiration time (binding time + 30 days) |

## 主键 / 索引
- 主键:`id`
- `idx_referee_user_id`:referee_user_id
- `idx_referral_code`:referral_code
- `idx_referrer_user_id`:referrer_user_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
