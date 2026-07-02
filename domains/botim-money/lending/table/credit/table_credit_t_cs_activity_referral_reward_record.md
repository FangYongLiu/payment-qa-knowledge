---
id: tbl_credit_t_cs_activity_referral_reward_record
object_type: Table
name: Referral reward record table (t_cs_activity_referral_reward_record)
aliases: [t_cs_activity_referral_reward_record, credit.t_cs_activity_referral_reward_record]
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

# Referral reward record table (t_cs_activity_referral_reward_record)

## 用途
物理表 `credit.t_cs_activity_referral_reward_record`,主键 `id`。Referral reward record table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | Primary key · 可空 |
| `activity_referral_relation_id` | int | Referral relation ID |
| `referrer_user_id` | varchar(20) | Referrer user ID · 可空 |
| `referee_user_id` | varchar(20) | Referee user ID · 可空 |
| `referee_status` | tinyint(2) | Referee status: 1. Signed up, 2. KYC passed, 3. KYC failed, 4. Application submitted, 5. Approved, 6. Disbursed, 7. Rejected |
| `referee_reward_type` | tinyint(1) | Referee reward type: 1. x% processing fee, 2. x% interest fee · 可空 |
| `referee_reward_amount` | decimal(15, 2) | Referee reward amount (NULL for coupon) · 可空 |
| `referee_reward_discount` | decimal(15, 2) | Referee coupon discount · 可空 |
| `referee_reward_coupon_id` | int | Referee coupon ID · 可空 |
| `referee_reward_status` | tinyint | Referee coupon usage status: 1/0 (whether used) · 可空 |
| `referee_coupon_used_time` | timestamp | Referee coupon used time · 可空 |
| `referee_coupon_expired_time` | timestamp | Referee coupon expiration time · 可空 |
| `referee_coupon_used_order_no` | varchar(64) | Referee coupon used order number · 可空 |
| `referrer_reward_type` | tinyint | 1=disbursement, 2=submit application · 可空 |
| `referrer_reward_amount` | decimal(15, 2) | Referrer reward amount (NULL for coupon) · 可空 |
| `referrer_reward_discount` | decimal(15, 2) | Referrer coupon discount · 可空 |
| `referrer_reward_status` | tinyint | Referrer reward status: 1/0 (whether utilized) · 可空 |
| `referrer_reward_coupon_id` | int | Referrer coupon ID · 可空 |
| `referrer_coupon_used_time` | timestamp | Referrer coupon used time · 可空 |
| `referrer_coupon_expired_time` | timestamp | Referrer coupon expiration time · 可空 |
| `referrer_cash_received_time` | timestamp | Referrer cash reward received time · 可空 |
| `created_time` | timestamp | Record creation time |

## 主键 / 索引
- 主键:`id`
- `idx_activity_referral_relation_id`:activity_referral_relation_id
- `idx_referee_coupon_expired_time`:referee_coupon_expired_time
- `idx_referee_reward_coupon_id`:referee_reward_coupon_id
- `idx_referee_user_id`:referee_user_id
- `idx_referrer_user_id`:referrer_user_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
