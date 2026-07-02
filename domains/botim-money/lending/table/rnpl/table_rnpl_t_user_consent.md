---
id: tbl_rnpl_t_user_consent
object_type: Table
name: Stores user consent for user (t_user_consent)
aliases: [t_user_consent, rnpl.t_user_consent]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: rnpl schema DDL
tags: [lending, rnpl]
sensitivity: normal
related_services: []
---

# Stores user consent for user (t_user_consent)

## 用途
物理表 `rnpl.t_user_consent`,主键 `consent_id`。Stores user consent for user。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `consent_id` | int | Unique ID for each consent record · 可空 |
| `user_id` | varchar(20) | Reference to the user who gave consent |
| `consent_type` | varchar(32) | Type of consent granted by the user |
| `consent_desc` | varchar(64) | Description of the consent type · 可空 |
| `consent_status` | varchar(32) | Indicates whether the CONSENT has ACTIVE or Deactive |
| `consent_timestamp` | timestamp | Timestamp when consent was given · 可空 |
| `expired_timestamp` | timestamp | Timestamp when consent was expire (NULL if still granted) · 可空 |
| `created_timestamp` | timestamp | Timestamp when consent was created · 可空 |

## 主键 / 索引
- 主键:`consent_id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
