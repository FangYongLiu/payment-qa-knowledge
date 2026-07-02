---
id: tbl_vis_t_migrate_record
object_type: Table
name: Unique index for migrate (t_migrate_record)
aliases: [t_migrate_record, vis.t_migrate_record]
domain: deposit-vam
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: vis schema DDL
tags: [deposit-vam, vis]
sensitivity: normal
related_services: []
---

# Unique index for migrate (t_migrate_record)

## 用途
物理表 `vis.t_migrate_record`,主键 `id`。Unique index for migrate。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key · 可空 |
| `file_id` | bigint(17) | File record ID · 可空 |
| `account_id` | int | VirtualAccount ID · 可空 |
| `member_id` | varchar(20) | Member ID · 可空 |
| `member_type` | char | Member type: C-Customer, M-Merchant · 可空 |
| `migrate_type` | char | Migrate type: M-Migrate, N-New · 可空 |
| `name` | varchar(32) | Member name · 可空 |
| `old_iban` | varchar(23) | Old IBAN (FAB, encrypted) · 可空 |
| `new_iban` | varchar(23) | New IBAN (PAYBY, backfilled after migration, encrypted) · 可空 |
| `email` | varchar(64) | Email · 可空 |
| `mobile` | varchar(32) | Mobile number · 可空 |
| `status` | varchar(2) | Status: P-Pending, I-In Progress, C-Completed, F-Failed, S-Skipped |
| `message` | varchar(255) | Message / error info · 可空 |
| `retry_count` | int | Retry count |
| `notify_status` | char | Notify status: null-Not sent, S-TodoCard sent, R-TodoCard removed · 可空 |
| `next_notify_time` | timestamp | Next scheduled notification time · 可空 |
| `extension` | varchar(512) | Extension info · 可空 |
| `gmt_create` | timestamp | Create time |
| `gmt_modified` | timestamp | Modified time |

## 主键 / 索引
- 主键:`id`
- `idx_file_id`:file_id
- `idx_migrate_mid`:member_id
- `idx_notify_status_next_time`:notify_status, next_notify_time
- `idx_status_member_type`:status, member_type, gmt_create

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
