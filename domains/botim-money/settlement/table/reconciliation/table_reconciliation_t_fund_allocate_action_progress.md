---
id: tbl_reconciliation_t_fund_allocate_action_progress
object_type: Table
name: Fund Allocate Action Progress (t_fund_allocate_action_progress)
aliases: [t_fund_allocate_action_progress, reconciliation.t_fund_allocate_action_progress]
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: reconciliation schema DDL
tags: [settlement, reconciliation]
sensitivity: normal
related_services: []
---

# Fund Allocate Action Progress (t_fund_allocate_action_progress)

## 用途
物理表 `reconciliation.t_fund_allocate_action_progress`,主键 `action_progress_id`。Fund Allocate Action Progress。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `action_progress_id` | bigint | Action Progress Id · 可空 |
| `action_progress_name` | varchar(32) | Action Progress Name |
| `sync_progress_id` | bigint | Sync Progress Id |
| `action_type` | char(3) | Action Type: ST-SettlementTransfer, NFS-netFundSettlement |
| `filter_rule` | varchar(512) | Filter Rule: JSON Format |
| `execute_param` | varchar(512) | Execute Param: JSON Format: templateId for ST, fundChannelCode for NFS · 可空 |
| `progress_time` | timestamp | Progress time: Current Progress Time |
| `sync_minutes` | int | Sync Minutes |
| `delay_minutes` | int | Delay Minutes: Query Delay Minutes |
| `next_trigger_time` | timestamp | Next trigger time |
| `enable_flag` | char | Enable flag: Y=Yes，N=No |
| `version` | bigint | Version |
| `extension` | varchar(255) | Extension · 可空 |
| `memo` | varchar(100) | Memo · 可空 |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`action_progress_id`
- `idx_enable_trigger_time`:enable_flag, next_trigger_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
