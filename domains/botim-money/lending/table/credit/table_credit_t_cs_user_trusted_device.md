---
id: tbl_credit_t_cs_user_trusted_device
object_type: Table
name: user device trust status table (t_cs_user_trusted_device)
aliases: [t_cs_user_trusted_device, credit.t_cs_user_trusted_device]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: credit schema DDL
tags: [lending, credit]
sensitivity: normal
related_services: []
---

# user device trust status table (t_cs_user_trusted_device)

## 用途
物理表 `credit.t_cs_user_trusted_device`,主键 `id`。user device trust status table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int(11) | id · 可空 |
| `user_id` | varchar(20) | user ID |
| `uniq_device_identifier` | varchar(64) | unique device identifier · 可空 |
| `device_id` | varchar(64) | device id |
| `device_name` | varchar(64) | device name · 可空 |
| `os_type` | varchar(50) | os type: iOS/android · 可空 |
| `os_version` | varchar(20) | os version · 可空 |
| `biometric_enabled` | tinyint(1) | biometric enabled, 1:enable 0:disable · 可空 |
| `trust_time` | timestamp | device trust time · 可空 |
| `last_login_at` | timestamp | last login time · 可空 |
| `distrust_time` | timestamp | device distrust time · 可空 |
| `trust_status` | tinyint(1) | device trust status: 0:distrust，1:trust |

## 主键 / 索引
- 主键:`id`
- `idx_user_id`:user_id

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
