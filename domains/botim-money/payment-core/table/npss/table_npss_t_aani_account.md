---
id: tbl_npss_t_aani_account
object_type: Table
name: aani account (t_aani_account)
aliases: [t_aani_account, npss.t_aani_account]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: npss schema DDL
tags: [payment-core, npss]
sensitivity: normal
related_services: []
---

# aani account (t_aani_account)

## 用途
物理表 `npss.t_aani_account`,主键 `aani_account_id`。aani account。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `aani_account_id` | bigint(19) | account id |
| `member_id` | varchar(20) | member id |
| `account_name` | varchar(32) | account name · 可空 |
| `account_type` | varchar(6) | account type: email,eid,mobile |
| `account_value` | varchar(32) | account value |
| `account_summary` | varchar(16) | account summary · 可空 |
| `status` | char | account status, A-available, D-deleted |
| `gmt_create` | timestamp(6) | create time |
| `gmt_modified` | timestamp(6) | modify time · 可空 |
| `gmt_last_trans` | timestamp(6) | last trans time · 可空 |

## 主键 / 索引
- 主键:`aani_account_id`
- `idx_aani_member_id`:member_id

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
