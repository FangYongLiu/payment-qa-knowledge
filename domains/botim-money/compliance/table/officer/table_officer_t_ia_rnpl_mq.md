---
id: tbl_officer_t_ia_rnpl_mq
object_type: Table
name: t_ia_rnpl_mq (t_ia_rnpl_mq)
aliases: [t_ia_rnpl_mq, officer.t_ia_rnpl_mq]
domain: compliance
status: active
owner: dewen.li
reviewer: dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: officer schema DDL
tags: [compliance, officer]
sensitivity: normal
related_services: []
---

# t_ia_rnpl_mq (t_ia_rnpl_mq)

## 用途
物理表 `officer.t_ia_rnpl_mq`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id  · 可空 |
| `create_by` | varchar(100) | creator · 可空 |
| `create_time` | timestamp | Creation time · 可空 |
| `update_by` | varchar(100) | Updater · 可空 |
| `update_time` | timestamp | Update time · 可空 |
| `application_id` | varchar(64) | app id |
| `task_name` | varchar(50) | Audit task name · 可空 |
| `broker_profile` | varchar(1000) | Broker information · 可空 |
| `check_item_po_list` | varchar(2000) | check_item_po_list · 可空 |
| `disbursement_po` | varchar(2000) | disbursement_po · 可空 |
| `loan_offer_po` | varchar(2000) | loan_offer_po · 可空 |
| `property_po` | varchar(1000) | Industry information · 可空 |
| `rent_contract_po` | varchar(2000) | rent_contract_po · 可空 |
| `tenant_profile` | varchar(1000) | Tenant information · 可空 |
| `user_quota_po` | varchar(1000) | Tenant rnpl account information · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
