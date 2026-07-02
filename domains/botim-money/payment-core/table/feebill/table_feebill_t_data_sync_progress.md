---
id: tbl_feebill_t_data_sync_progress
object_type: Table
name: Data Sync Progress (t_data_sync_progress)
aliases: [t_data_sync_progress, feebill.t_data_sync_progress]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: feebill schema DDL
tags: [payment-core, feebill]
sensitivity: normal
related_services: []
---

# Data Sync Progress (t_data_sync_progress)

## 用途
物理表 `feebill.t_data_sync_progress`,主键 `progress_id`。Data Sync Progress。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `progress_id` | int | Progress Id · 可空 |
| `app_code` | varchar(64) | App Code |
| `simple_app_code` | varchar(10) | Simple App Code |
| `sync_source` | varchar(32) | Sync Source · 可空 |
| `interval_minutes` | int | Interval Minutes |
| `delay_minutes` | int | Delay Minutes |
| `next_trigger_time` | timestamp | Next Trigger Time |
| `gmt_sync_begin` | timestamp | Sync Begin Time |
| `gmt_sync_end` | timestamp | Sync End Time |
| `data_index` | int | Data Index |
| `page_size` | int | Page Size |
| `error_msg` | varchar(1024) | Error Message · 可空 |
| `update_version` | bigint | Update Version |
| `enable_flag` | char | Enable flag: Y=Yes，N=No |
| `extension` | varchar(255) | Extension · 可空 |
| `memo` | varchar(100) | Memo · 可空 |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`progress_id`
- `uk_app_code_sync_source`:app_code, sync_source (UNIQUE)
- `uk_simple_app_code_sync_source`:simple_app_code, sync_source

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
