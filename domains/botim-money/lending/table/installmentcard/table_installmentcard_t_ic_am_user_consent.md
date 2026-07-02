---
id: tbl_installmentcard_t_ic_am_user_consent
object_type: Table
name: User consent records for installment card (t_ic_am_user_consent)
aliases: [t_ic_am_user_consent, installmentcard.t_ic_am_user_consent]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: installmentcard schema DDL
tags: [lending, installmentcard]
sensitivity: normal
related_services: []
---

# User consent records for installment card (t_ic_am_user_consent)

## 用途
物理表 `installmentcard.t_ic_am_user_consent`,主键 `id`。User consent records for installment card。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key · 可空 |
| `member_id` | varchar(32) | External member/customer identifier |
| `consent` | varchar(64) | Consent type name (e.g. TERMS_AND_CONDITIONS, DATA_PRIVACY, KEY_FACT_STATEMENT, CREDIT_AGREEMENT, DIRECT_DEBIT_AGREEMENT, COOLING_OFF_PERIOD_WAIVER) |
| `create_time` | datetime | Row created time |
| `update_time` | datetime | Row last updated time |

## 主键 / 索引
- 主键:`id`
- `uk_member_consent`:member_id, consent (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
