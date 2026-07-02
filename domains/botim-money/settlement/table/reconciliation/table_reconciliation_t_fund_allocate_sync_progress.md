---
id: tbl_reconciliation_t_fund_allocate_sync_progress
object_type: Table
name: Fund Allocate Sync Progress (t_fund_allocate_sync_progress)
aliases: [t_fund_allocate_sync_progress, reconciliation.t_fund_allocate_sync_progress]
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

# Fund Allocate Sync Progress (t_fund_allocate_sync_progress)

## 用途
物理表 `reconciliation.t_fund_allocate_sync_progress`,主键 `sync_progress_id`。Fund Allocate Sync Progress。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `sync_progress_id` | bigint | Sync Progress Id · 可空 |
| `sync_progress_name` | varchar(32) | Sync Progress Name |
| `bank_code` | varchar(32) | Bank Code |
| `account_id` | varchar(32) | Account Id |
| `progress_time` | timestamp | Progress time: Current Progress Time |
| `sync_minutes` | int | Sync Minutes |
| `delay_minutes` | int | Delay minutes: Query Delay Minutes |
| `next_trigger_time` | timestamp | Next trigger time |
| `current_page` | int | Current Page: Current Query Page |
| `page_size` | int | Page Size |
| `enable_flag` | char | Enable Flag |
| `version` | bigint | Version |
| `extension` | varchar(255) | Extension · 可空 |
| `memo` | varchar(255) | Memo · 可空 |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`sync_progress_id`
- `uk_bank_account`:bank_code, account_id (UNIQUE)
- `idx_enable_trigger_time`:enable_flag, next_trigger_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
