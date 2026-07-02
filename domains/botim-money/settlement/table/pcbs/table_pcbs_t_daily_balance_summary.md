---
id: tbl_pcbs_t_daily_balance_summary
object_type: Table
name: Daily Balance Summary (t_daily_balance_summary)
aliases: [t_daily_balance_summary, pcbs.t_daily_balance_summary]
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: pcbs schema DDL
tags: [settlement, pcbs]
sensitivity: normal
related_services: []
---

# Daily Balance Summary (t_daily_balance_summary)

## 用途
物理表 `pcbs.t_daily_balance_summary`,主键 `summary_id`。Daily Balance Summary。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `summary_id` | bigint | Summary ID |
| `file_id` | bigint | File ID |
| `origin_amount` | decimal(19, 4) | Origin Amount |
| `origin_currency` | char(3) | Origin Currency |
| `local_amount` | decimal(19, 4) | Local Amount |
| `local_currency` | char(3) | Local Currency |
| `exchange_rate` | decimal(19, 8) | Exchange Rate |
| `extension` | varchar(255) | Extension · 可空 |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`summary_id`
- `uk_file_id_origin_currency`:file_id, origin_currency (UNIQUE)
- `idx_update_time`:update_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
