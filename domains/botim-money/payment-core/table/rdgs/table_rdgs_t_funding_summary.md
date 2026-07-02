---
id: tbl_rdgs_t_funding_summary
object_type: Table
name: funding summary (t_funding_summary)
aliases: [t_funding_summary, rdgs.t_funding_summary]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: rdgs schema DDL
tags: [payment-core, rdgs]
sensitivity: normal
related_services: []
---

# funding summary (t_funding_summary)

## 用途
物理表 `rdgs.t_funding_summary`,主键 `id`。funding summary。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id |
| `task_id` | bigint | task id |
| `file_tag` | varchar(64) | file tag |
| `channel_code` | varchar(20) | channel code |
| `channel_name` | varchar(100) | channel name |
| `country_code` | char(3) | country code |
| `country_name` | varchar(100) | country name |
| `opening_balance` | decimal(19, 4) | opening balance |
| `closing_balance` | decimal(19, 4) | closing balance |
| `total_funding_amount` | decimal(19, 4) | total funding amount |
| `total_dealing_cash` | decimal(19, 4) | total dealing cash · 可空 |
| `total_dealing_tom` | decimal(19, 4) | total dealing tom · 可空 |
| `total_dealing_spot` | decimal(19, 4) | total dealing spot · 可空 |
| `total_payment_amount` | decimal(19, 4) | total payment amount · 可空 |
| `total_cancelled_amount` | decimal(19, 4) | total cancelled amount · 可空 |
| `currency` | char(3) | currency · 可空 |
| `summary_date` | datetime | summary date |
| `start_time` | timestamp | start time |
| `end_time` | timestamp | end time |
| `extension` | varchar(255) | Extension · 可空 |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
