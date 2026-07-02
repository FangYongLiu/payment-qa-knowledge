---
id: tbl_ppc_t_sync_progress
object_type: Table
name: Sync Progress (t_sync_progress)
aliases: [t_sync_progress, ppc.t_sync_progress]
domain: card
status: active
owner: jianfei.wang
reviewer: jianfei.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ppc schema DDL
tags: [card, ppc]
sensitivity: normal
related_services: []
---

# Sync Progress (t_sync_progress)

## 用途
物理表 `ppc.t_sync_progress`,主键 `progress_id`。Sync Progress。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `progress_id` | bigint | Progress Id: 8 + 9 digits |
| `virtual_card_id` | bigint | Current Virtual Card Id |
| `member_type` | char | Member Type: P=Personal, C=Corporation · 可空 |
| `progress_status` | char | Sync Status: I=Init，N=Normal, C=Close |
| `account_no` | varchar(32) | Account No · 可空 |
| `sync_version` | bigint | Sync Accounting Version · 可空 |
| `processing_detail_id` | bigint | Processing Detail Id · 可空 |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`progress_id`
- `uk_virtual_card_id`:virtual_card_id (UNIQUE)
- `idx_account_no`:account_no
- `idx_update_time`:update_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
