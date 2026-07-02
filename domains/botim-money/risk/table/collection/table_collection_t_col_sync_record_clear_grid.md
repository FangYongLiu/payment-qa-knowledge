---
id: tbl_collection_t_col_sync_record_clear_grid
object_type: Table
name: Synchronize the collection bill record sheet to ClearGrid (t_col_sync_record_clear_grid)
aliases: [t_col_sync_record_clear_grid, collection.t_col_sync_record_clear_grid]
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

# Synchronize the collection bill record sheet to ClearGrid (t_col_sync_record_clear_grid)

## 用途
物理表 `collection.t_col_sync_record_clear_grid`,主键 `id`。Synchronize the collection bill record sheet to ClearGrid。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint unsigned | primary key · 可空 |
| `create_by` | varchar(100) | creator · 可空 |
| `create_time` | timestamp | creation time · 可空 |
| `update_time` | timestamp | update time · 可空 |
| `update_by` | varchar(100) | update personnel · 可空 |
| `bill_no` | varchar(64) | bill number |
| `order_no` | varchar(64) | Order Number |
| `member_id` | varchar(20) | Member ID |
| `batch_id` | varchar(50) | Batch id |
| `sync_type` | tinyint | Synchronization types: 1= Create, 2= Modify, 3= Withdraw · 可空 |
| `sync_time` | timestamp | Synchronization time · 可空 |
| `sync_status` | tinyint | Synchronization status: initial = 0,1 = success, 2= failure |
| `failure_reasons` | varchar(255) | Reasons for failure · 可空 |
| `repay_capital` | decimal(19, 2) | Repay principal · 可空 |
| `repay_interest` | decimal(19, 2) | Repay intrerest · 可空 |
| `repay_fee` | decimal(19, 2) | Repay fee · 可空 |
| `paid_amount` | decimal(19, 2) | Repay amount · 可空 |
| `will_repay_penalty` | decimal(19, 2) | Will repay penalty · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_batch_id`:batch_id
- `idx_bill_no`:bill_no
- `idx_order_no`:order_no

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
