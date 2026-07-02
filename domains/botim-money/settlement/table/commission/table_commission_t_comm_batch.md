---
id: tbl_commission_t_comm_batch
object_type: Table
name: Commission Batch (t_comm_batch)
aliases: [t_comm_batch, commission.t_comm_batch]
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: commission schema DDL
tags: [settlement, commission]
sensitivity: normal
related_services: []
---

# Commission Batch (t_comm_batch)

## 用途
物理表 `commission.t_comm_batch`,主键 `batch_id`。Commission Batch。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `batch_id` | bigint | Batch id: 8 date + 9 sequence · 可空 |
| `comm_progress_id` | bigint | Comm progress id |
| `sync_begin_time` | timestamp | Sync begin time |
| `sync_end_time` | timestamp | Sync end time |
| `batch_status` | varchar(10) | Batch Status: MP=Mark Process, SP=Summary Process, C=Completed |
| `extension` | varchar(255) | Extension: tradeSplitMinustes, refundSplitMinutes · 可空 |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`batch_id`
- `idx_progress_i`:comm_progress_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
