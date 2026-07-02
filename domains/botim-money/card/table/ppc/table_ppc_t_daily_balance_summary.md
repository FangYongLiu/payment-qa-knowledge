---
id: tbl_ppc_t_daily_balance_summary
object_type: Table
name: Daily Balance Summary (t_daily_balance_summary)
aliases: [t_daily_balance_summary, ppc.t_daily_balance_summary]
domain: card
status: active
owner: jianfei.wang
reviewer: jianfei.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ppc schema DDL
tags: [card, ppc]
sensitivity: normal
related_services: []
---

# Daily Balance Summary (t_daily_balance_summary)

## 用途
物理表 `ppc.t_daily_balance_summary`,主键 `summary_id`。Daily Balance Summary。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `summary_id` | bigint | Summary id · 可空 |
| `file_id` | bigint | File id |
| `account_date` | char(8) | Account date |
| `currency` | char(3) | Currency |
| `file_detail_count` | int | File detail count |
| `file_sum_amount` | decimal(19, 4) | File sum amount |
| `actual_detail_count` | int | Actual detail count |
| `diff_count` | int | Different count |
| `summary_status` | char(2) | Summary status: CP=Check Processing, CC=Check Complete |
| `check_process` | bigint | Check process · 可空 |
| `memo` | varchar(100) | Memo · 可空 |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`summary_id`
- `uk_file_id_currency`:file_id, currency (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
