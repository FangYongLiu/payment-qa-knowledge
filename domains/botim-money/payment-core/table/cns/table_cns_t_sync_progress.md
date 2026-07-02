---
id: tbl_cns_t_sync_progress
object_type: Table
name: Sync Progress Table - Track batch sync cursor and status (t_sync_progress)
aliases: [t_sync_progress, cns.t_sync_progress]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: cns schema DDL
tags: [payment-core, cns]
sensitivity: normal
related_services: []
---

# Sync Progress Table - Track batch sync cursor and status (t_sync_progress)

## 用途
物理表 `cns.t_sync_progress`,主键 `progress_id`。Sync Progress Table - Track batch sync cursor and status。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `progress_id` | bigint | Auto-increment primary key · 可空 |
| `business_type` | varchar(32) | Business Type: FIRST_DEPOSIT_USER |
| `sync_status` | char | Sync Status: R=Running, C=Closed |
| `sync_version` | bigint | Sync Version |
| `cursor_time` | timestamp | Cursor - Last processed GMT_MODIFIED · 可空 |
| `cursor_voucher_no` | varchar(32) | Cursor - Last processed TRADE_VOUCHER_NO · 可空 |
| `total_processed_count` | int | Total processed record count |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`progress_id`
- `uk_business_type`:business_type (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
