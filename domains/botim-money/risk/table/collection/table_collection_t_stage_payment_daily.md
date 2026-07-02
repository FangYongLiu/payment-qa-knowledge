---
id: tbl_collection_t_stage_payment_daily
object_type: Table
name: Daily stageQuery repay buckets (pre-aggregated) (t_stage_payment_daily)
aliases: [t_stage_payment_daily, collection.t_stage_payment_daily]
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: collection schema DDL
tags: [risk, collection]
sensitivity: normal
related_services: []
---

# Daily stageQuery repay buckets (pre-aggregated) (t_stage_payment_daily)

## 用途
物理表 `collection.t_stage_payment_daily`,主键 `id`。Daily stageQuery repay buckets (pre-aggregated)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Surrogate primary key · 可空 |
| `stat_date` | date | Business calendar date (stageParamDate) |
| `dept_id` | int | -1 = company-wide row; otherwise department id |
| `product_code` | int | Product code (single selection on UI) |
| `stage` | varchar(12) | Collection stage label (Stage column; StageEnum.value) |
| `query_type` | tinyint | 1 = Amount mode; 2 = Account (count) mode |
| `restructure` | tinyint | 0 = normal; 1 = restructure (productTag=restructure) |
| `amt_am0` | decimal(20, 4) | Repay amount 0am-9am (HOUR(repay_time) 0-8); UI column 0am-9am |
| `amt_am9` | decimal(20, 4) | Repay amount 9am-10am; UI column 9am-10am |
| `amt_am10` | decimal(20, 4) | Repay amount 10am-11am; UI column 10am-11am |
| `amt_am11` | decimal(20, 4) | Repay amount 11am-12am; UI column 11am-12am |
| `amt_am12` | decimal(20, 4) | Repay amount 12am-13pm; UI column 12am-13pm |
| `amt_pm1` | decimal(20, 4) | Repay amount 13pm-14pm; UI column 13pm-14pm |
| `amt_pm2` | decimal(20, 4) | Repay amount 14pm-15pm; UI column 14pm-15pm |
| `amt_pm3` | decimal(20, 4) | Repay amount 15pm-16pm; UI column 15pm-16pm |
| `amt_pm4` | decimal(20, 4) | Repay amount 16pm-17pm; UI column 16pm-17pm |
| `amt_pm5` | decimal(20, 4) | Repay amount 17pm-18pm; UI column 17pm-18pm |
| `amt_pm6` | decimal(20, 4) | Repay amount 18pm-19pm; UI column 18pm-19pm |
| `amt_pm7` | decimal(20, 4) | Repay amount 19pm-24pm (HOUR > 18); UI column 19pm-24pm |
| `amt_total` | decimal(20, 4) | Sum of hourly buckets for that stage/day; UI Total column |
| `version` | int | Row version; incremented on upsert |
| `created_at` | datetime | Insert time |
| `updated_at` | datetime | Last update time |

## 主键 / 索引
- 主键:`id`
- `uk_rpt_stage_day`:stat_date, dept_id, product_code (UNIQUE)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
