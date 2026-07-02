---
id: tbl_commission_t_comm_batch_progress
object_type: Table
name: Commission Progress (t_comm_batch_progress)
aliases: [t_comm_batch_progress, commission.t_comm_batch_progress]
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

# Commission Progress (t_comm_batch_progress)

## 用途
物理表 `commission.t_comm_batch_progress`,主键 `comm_progress_id`。Commission Progress。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `comm_progress_id` | bigint | Comm progress id · 可空 |
| `sync_progress_id` | bigint | Sync progress id |
| `partner_id` | varchar(20) | Partner id |
| `group_type` | varchar(10) | Group type: BPC=Biz product code, PSC=Product set code |
| `group_code` | varchar(50) | Group code |
| `progress_time` | timestamp | Progress time |
| `comm_minutes` | bigint | Commission minutes |
| `delay_minutes` | bigint | Delay minutes |
| `next_trigger_time` | timestamp | Next trigger time |
| `enable_flag` | char | Enable flag: Y=Yes, N=No |
| `current_batch_id` | bigint | Current batch id · 可空 |
| `commission_type` | varchar(10) | C/R · 可空 |
| `extension` | varchar(255) | Extension · 可空 |
| `memo` | varchar(100) | Memo · 可空 |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`comm_progress_id`
- `idx_next_trigger_time`:next_trigger_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
