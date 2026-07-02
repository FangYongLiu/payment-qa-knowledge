---
id: tbl_credit_t_cs_activity_referrer_code
object_type: Table
name: Referrer code for each referrer (t_cs_activity_referrer_code)
aliases: [t_cs_activity_referrer_code, credit.t_cs_activity_referrer_code]
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

# Referrer code for each referrer (t_cs_activity_referrer_code)

## 用途
物理表 `credit.t_cs_activity_referrer_code`,主键 `id`。Referrer code for each referrer。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | Primary key · 可空 |
| `referrer_user_id` | varchar(20) | Referrer user ID |
| `referrer_user_nationality` | varchar(64) | referrer user nationality · 可空 |
| `reward_id` | int | Reward ID · 可空 |
| `referral_code` | varchar(6) | Referral code · 可空 |
| `is_frozen` | tinyint(1) | 0: Not frozen, 1: Frozen · 可空 |
| `created_time` | timestamp | Creation time |
| `updated_time` | timestamp | Update time · 可空 |
| `is_in_blacklist` | tinyint | 0: Not in blacklist, 1: In blacklist · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_referral_code`:referral_code
- `idx_referrer_user_id`:referrer_user_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
