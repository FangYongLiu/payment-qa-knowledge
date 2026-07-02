---
id: tbl_ppc_t_deactivate_card_record
object_type: Table
name: Deactivate card record table (t_deactivate_card_record)
aliases: [t_deactivate_card_record, ppc.t_deactivate_card_record]
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

# Deactivate card record table (t_deactivate_card_record)

## 用途
物理表 `ppc.t_deactivate_card_record`,主键 `id`。Deactivate card record table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary Key · 可空 |
| `member_id` | varchar(20) | Member ID |
| `virtual_card_id` | bigint | Virtual card id · 可空 |
| `virtual_card_type` | char(2) | Virtual card type (MC=Multi-Currency, PR=Payroll Card) |
| `handle_status` | char | Member processing status (P=PROCESSING, S=SUCCESSFUL, F=FAILED) |
| `handle_type` | char | Member handle type (S=Silently handle card) |
| `handle_result` | varchar(255) | Member processing result · 可空 |
| `handle_times` | int | Handle times count |
| `extension` | varchar(128) | Extended fields (JSON storage) · 可空 |
| `create_time` | timestamp | Creation time |
| `update_time` | timestamp | Update time |
| `retry_time` | timestamp | Next retry time · 可空 |
| `create_name` | varchar(64) | Creator name |
| `update_name` | varchar(64) | Updater name · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_member_id`:member_id
- `idx_retry_time_handle_status`:retry_time, handle_status
- `idx_update_time_member_id`:update_time, member_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
