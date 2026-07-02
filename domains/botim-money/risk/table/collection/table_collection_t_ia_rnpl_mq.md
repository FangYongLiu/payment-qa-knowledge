---
id: tbl_collection_t_ia_rnpl_mq
object_type: Table
name: rnpl_application_snapshot (t_ia_rnpl_mq)
aliases: [t_ia_rnpl_mq, collection.t_ia_rnpl_mq]
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

# rnpl_application_snapshot (t_ia_rnpl_mq)

## 用途
物理表 `collection.t_ia_rnpl_mq`,主键 `id`。rnpl_application_snapshot。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id · 可空 |
| `create_by` | varchar(64) | create_by · 可空 |
| `create_time` | timestamp | create_time · 可空 |
| `update_by` | varchar(64) | update_by · 可空 |
| `update_time` | timestamp | update_time · 可空 |
| `application_id` | varchar(64) | application_id |
| `task_name` | varchar(50) | task_name · 可空 |
| `broker_profile` | varchar(1000) | breker_info · 可空 |
| `check_item_po_list` | text | check_item_po_list · 可空 |
| `disbursement_po` | text | disbursement_po · 可空 |
| `loan_offer_po` | text | loan_offer_po · 可空 |
| `property_po` | varchar(1000) | property_po · 可空 |
| `rent_contract_po` | text | rent_contract_po · 可空 |
| `tenant_profile` | varchar(1000) | tenant_profile · 可空 |
| `user_quota_po` | varchar(1000) | user_quota_po · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_application_id`:application_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
