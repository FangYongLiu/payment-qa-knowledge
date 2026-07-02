---
id: tbl_adg_t_system_generated_user
object_type: Table
name: System generated user identity mapping (t_system_generated_user)
aliases: [t_system_generated_user, adg.t_system_generated_user]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: adg schema DDL
tags: [marketing, adg]
sensitivity: normal
related_services: []
---

# System generated user identity mapping (t_system_generated_user)

## 用途
物理表 `adg.t_system_generated_user`,主键 `id`。System generated user identity mapping。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Auto-generated primary key · 可空 |
| `identity_hash` | varchar(32) | MD5 hash of identity (EID for individual, EID|TradeLicense|Authority for non-individual) |
| `create_at` | timestamp | Record creation timestamp · 可空 |

## 主键 / 索引
- 主键:`id`
- `uk_identity_hash`:identity_hash (UNIQUE)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
