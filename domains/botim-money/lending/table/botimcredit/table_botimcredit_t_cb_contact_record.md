---
id: tbl_botimcredit_t_cb_contact_record
object_type: Table
name: User contract signing record table (t_cb_contact_record)
aliases: [t_cb_contact_record, botimcredit.t_cb_contact_record]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: botimcredit schema DDL
tags: [lending, botimcredit]
sensitivity: normal
related_services: []
---

# User contract signing record table (t_cb_contact_record)

## 用途
物理表 `botimcredit.t_cb_contact_record`,主键 `id`。User contract signing record table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 待补 · 可空 |
| `user_id` | varchar(32) | User ID |
| `contact_tem_id` | int | Contract template ID |
| `data` | varchar(1000) | Variable data in the contract · 可空 |
| `notify_status` | smallint | 0: Notification not sent; 1: Notification sent successfully |
| `create_time` | timestamp | 待补 |
| `update_time` | timestamp | 待补 · 可空 |
| `file_tag` | varchar(128) | Path of the contract file in the UFS system · 可空 |
| `scene` | varchar(32) | First activation: activate; Re-sign auto debit: resign_auto_debit |

## 主键 / 索引
- 主键:`id`
- `ix_t`:create_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
