---
id: tbl_reconciliation_t_fund_allocate_action_batch
object_type: Table
name: Fund Allocate Action Batch (t_fund_allocate_action_batch)
aliases: [t_fund_allocate_action_batch, reconciliation.t_fund_allocate_action_batch]
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

# Fund Allocate Action Batch (t_fund_allocate_action_batch)

## 用途
物理表 `reconciliation.t_fund_allocate_action_batch`,主键 `action_batch_id`。Fund Allocate Action Batch。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `action_batch_id` | bigint | Action Batch Id: 8 digits date + 9 digits sequence |
| `action_progress_id` | int | Action Progress Id |
| `sync_begin_time` | timestamp | Sync Begin Time |
| `sync_end_time` | timestamp | Sync End Time |
| `total_records` | int | Total Records · 可空 |
| `total_amount` | decimal(19, 4) | Total Amount · 可空 |
| `currency` | char(3) | Currency · 可空 |
| `related_identity` | varchar(50) | Related Identity: settlement detalId, netSettlement flowId · 可空 |
| `status` | char | Status: I-Initial R-Data Ready F-Fail S-Success |
| `extension` | varchar(255) | Extension · 可空 |
| `memo` | varchar(255) | Memo · 可空 |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`action_batch_id`
- `uk_actionid_synctime`:action_progress_id, sync_begin_time, sync_end_time (UNIQUE)
- `idx_related_identity`:related_identity

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
