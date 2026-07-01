---
id: tbl_remittance_t_dyn_strategy_stat
object_type: Table
domain: remittance
status: active
owner: lei.pan
reviewer: lei.pan
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (remittance schema) 2026-06-25
tags:
- remittance
- remittance
- t_dyn_strategy_stat
subdomain: remittance
module: null
sensitivity: normal
name: Dynamic Pricing - Strategy Statistics Table(t_dyn_strategy_stat)
aliases:
- t_dyn_strategy_stat
related_services:
- svc_remittance
related_scenarios: []
---
# Dynamic Pricing - Strategy Statistics Table(t_dyn_strategy_stat)

## 用途
Dynamic Pricing - Strategy Statistics Table。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | Primary Key |
| `strategy_id` | bigint | NOT NULL | Strategy ID (策略ID) |
| `biz_key` | varchar(64) | NOT NULL | Business Key (统计维度标识) |
| `biz_value` | varchar(64) | NOT NULL | Business Value (统计维度值) |
| `time_window` | varchar(16) | 默认 'ALL' | Time Window (ALL/LAST_7D/LAST_30D/LAST_90D/LAST_1Y) |
| `gmt_create` | timestamp | NOT NULL / 默认 CURRENT_TIMESTAMP | Creation Time |
| `gmt_modified` | timestamp | NOT NULL / 默认 CURRENT_TIMESTAMP | Last Modification Time |

## 主键 / 索引
- 主键:(`id`)
- 唯一约束:
  - `uk_strategy_biz_key_time` 唯一 (strategy_id, biz_key, time_window)
- 索引:
  - `idx_biz_key` (biz_key)
  - `idx_strategy_id` (strategy_id)
  - `idx_time_window` (time_window)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
