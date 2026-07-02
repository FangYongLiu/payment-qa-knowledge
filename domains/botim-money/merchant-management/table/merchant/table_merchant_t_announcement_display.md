---
id: tbl_merchant_t_announcement_display
object_type: Table
name: Tracks when pop-up announcements are displayed to merchants (t_announcement_display)
aliases: [t_announcement_display, merchant.t_announcement_display]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: merchant schema DDL
tags: [merchant-management, merchant]
sensitivity: normal
related_services: []
---

# Tracks when pop-up announcements are displayed to merchants (t_announcement_display)

## 用途
物理表 `merchant.t_announcement_display`,主键 `id`。Tracks when pop-up announcements are displayed to merchants。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key · 可空 |
| `announcement_id` | bigint | Reference to the announcement |
| `merchant_id` | varchar(20) | Merchant ID who viewed the announcement |
| `session_id` | varchar(100) | Session ID (optional, used for SHOW_EVERY_SESSION tracking) · 可空 |
| `display_time` | datetime | Timestamp when the pop-up was displayed |
| `created_time` | timestamp | Record creation time · 可空 |
| `last_updated_time` | timestamp | Last update time · 可空 |
| `data_version` | bigint | Version number · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_announcement_merchant`:announcement_id, merchant_id
- `idx_merchant_session`:merchant_id, session_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
