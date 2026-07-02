---
id: tbl_credit_t_cs_activity_record
object_type: Table
name: activity record table (t_cs_activity_record)
aliases: [t_cs_activity_record, credit.t_cs_activity_record]
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

# activity record table (t_cs_activity_record)

## 用途
物理表 `credit.t_cs_activity_record`,主键 `id`。activity record table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | primary key · 可空 |
| `activity_id` | int | activity code |
| `activity_code` | varchar(64) | share code |
| `user_id` | varchar(32) | user ID |
| `coupon_id` | int | coupon ID |
| `reward_type` | tinyint | reward type |
| `reward_amount` | decimal(15, 2) | reward amount · 可空 |
| `reward_discount` | decimal(15, 2) | reward discount · 可空 |
| `expired_time` | timestamp | coupon expired time |
| `order_no` | varchar(64) | order no · 可空 |
| `coupon_used_time` | timestamp | coupon used time · 可空 |
| `created_time` | timestamp | created time |
| `status` | tinyint | status：0:init，1:used |
| `type` | tinyint | type：1:buyback |

## 主键 / 索引
- 主键:`id`
- `idx_user_id_activity_id`:user_id, activity_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
