---
id: tbl_household_t_hh_contract_protocol
object_type: Table
name: contract protocol (t_hh_contract_protocol)
aliases: [t_hh_contract_protocol, household.t_hh_contract_protocol]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: household schema DDL
tags: [merchant-management, household]
sensitivity: normal
related_services: []
---

# contract protocol (t_hh_contract_protocol)

## 用途
物理表 `household.t_hh_contract_protocol`,主键 `id`。contract protocol。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | ulid |
| `signer_id` | varchar(32) | wallet owner id |
| `contract_id` | varchar(32) | contract id |
| `deduct_protocol_no` | varchar(32) | deduct protocol no |
| `pay_code` | varchar(8) | pay code |
| `pay_method` | varchar(10) | pay method:|Balance|CardType| |
| `card_type` | varchar(10) | card type:|Credit|Debit| · 可空 |
| `last_four` | varchar(4) | last four · 可空 |
| `create_at` | timestamp | create time |
| `update_at` | timestamp | update time |

## 主键 / 索引
- 主键:`id`
- `idx_contract_id`:contract_id

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
