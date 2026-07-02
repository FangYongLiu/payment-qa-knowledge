---
id: tbl_feebill_t_data_sync_progress_his
object_type: Table
name: Data Sync Progress History (t_data_sync_progress_his)
aliases: [t_data_sync_progress_his, feebill.t_data_sync_progress_his]
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

# Data Sync Progress History (t_data_sync_progress_his)

## 用途
物理表 `feebill.t_data_sync_progress_his`,主键 `his_id`。Data Sync Progress History。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `his_id` | bigint | History Id · 可空 |
| `app_code` | varchar(64) | App Code |
| `progress_id` | int | Progress Id |
| `gmt_sync_begin` | timestamp | Sync Begin Time |
| `gmt_sync_end` | timestamp | Sync End Time |
| `data_count` | bigint | Data Count |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`his_id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
