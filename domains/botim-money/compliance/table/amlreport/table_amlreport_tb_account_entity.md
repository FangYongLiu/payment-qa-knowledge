---
id: tbl_amlreport_tb_account_entity
object_type: Table
name: 账户实体表 (tb_account_entity)
aliases: [tb_account_entity, amlreport.tb_account_entity]
domain: compliance
status: active
owner: dewen.li
reviewer: dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: amlreport schema DDL
tags: [compliance, amlreport]
sensitivity: normal
related_services: []
---

# 账户实体表 (tb_account_entity)

## 用途
物理表 `amlreport.tb_account_entity`,主键 `id`。账户实体表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主键 · 可空 |
| `member_id` | varchar(32) | 会员ID · 可空 |
| `entity_value` | varchar(128) | 实体值 · 可空 |
| `entity_type` | varchar(20) | 实体类型 Bank card  / IBAN / Device ID · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_account_entity_value`:entity_value

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
