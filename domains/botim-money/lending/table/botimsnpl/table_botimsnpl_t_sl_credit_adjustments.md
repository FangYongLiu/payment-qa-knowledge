---
id: tbl_botimsnpl_t_sl_credit_adjustments
object_type: Table
name: credit limit adjustment table (t_sl_credit_adjustments)
aliases: [t_sl_credit_adjustments, botimsnpl.t_sl_credit_adjustments]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: botimsnpl schema DDL
tags: [lending, botimsnpl]
sensitivity: normal
related_services: []
---

# credit limit adjustment table (t_sl_credit_adjustments)

## 用途
物理表 `botimsnpl.t_sl_credit_adjustments`,主键 `id`。credit limit adjustment table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | unique id · 可空 |
| `user_id` | varchar(20) | user id |
| `credit_id` | bigint | relate credit table |
| `adjust_type` | tinyint | adjust type[1(permanent increase),2(temporary increase),3(permanent decrease),4(frozen)] |
| `before_amount` | decimal(15, 2) | amount before adjustment |
| `adjust_amount` | decimal(15, 2) | amount of adjustment |
| `after_amount` | decimal(15, 2) | amount after adjustment |
| `effective_time` | timestamp | adjustment effective time |
| `status` | varchar(12) | PENDING/PROCESSING/SUCCESS/FAILED |
| `expire_time` | timestamp | adjustment expire time(for temporary increase) · 可空 |
| `operator_id` | bigint | operator id |
| `operator_name` | varchar(64) | operator name |
| `reason_code` | varchar(32) | adjustment reason code |
| `reason_desc` | varchar(255) | adjustment reason description · 可空 |
| `review_id` | bigint | review task id · 可空 |
| `ext` | varchar(200) | ext · 可空 |
| `created_time` | timestamp | created time |
| `last_modified` | timestamp | last modified time |
| `request_id` | varchar(64) | Unique request identifier received from Risk system (used for deduplication) |
| `version` | varchar(64) | Risk batch identifier generated using etl_dt_currentTimeStamp (format: YYYYMMDD_timestamp) · 可空 |
| `request_source` | tinyint | Source of request: 0 = Quantix, 1 = Risk · 可空 |
| `cohort_name` | varchar(64) | Cohort label for tracking campaigns (e.g., May-2026-Limit-Increase) · 可空 |
| `offer_shown` | tinyint(1) | Flag to indicate if increased limit UI was shown to user (0 = No, 1 = Yes) · 可空 |
| `offer_shown_at` | datetime | Timestamp when user first saw the increased limit UI · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_cradj_create_time`:created_time
- `idx_cradj_credit_id`:credit_id
- `idx_cradj_review_id`:review_id
- `idx_cradj_user_id`:user_id
- `idx_request_id`:request_id
- `idx_version`:version

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
