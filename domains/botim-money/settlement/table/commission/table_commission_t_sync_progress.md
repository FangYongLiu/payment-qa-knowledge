---
id: tbl_commission_t_sync_progress
object_type: Table
name: Sync Progress (t_sync_progress)
aliases: [t_sync_progress, commission.t_sync_progress]
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

# Sync Progress (t_sync_progress)

## 用途
物理表 `commission.t_sync_progress`,主键 `sync_progress_id`。Sync Progress。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `sync_progress_id` | bigint | Sync progress id · 可空 |
| `partner_id` | varchar(20) | Partner id |
| `group_type` | varchar(10) | Group type: BPC=Biz product code, PSC=Product set code |
| `group_code` | varchar(50) | Group code |
| `progress_time` | timestamp | Progress time |
| `sync_minutes` | bigint | Sync minutes |
| `delay_minutes` | bigint | Delay minutes |
| `next_trigger_time` | timestamp | Next trigger time |
| `config_status` | char | Config status: Y=Enabled, N=Disabled, E=Error Disabled |
| `version` | bigint | Version |
| `extension` | varchar(255) | Extension · 可空 |
| `memo` | varchar(100) | Memo · 可空 |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`sync_progress_id`
- `uk_partner_id_product_set`:partner_id, group_type, group_code (UNIQUE)
- `idx_trigger_time_status`:next_trigger_time, config_status

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
