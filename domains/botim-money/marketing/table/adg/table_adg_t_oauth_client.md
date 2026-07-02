---
id: tbl_adg_t_oauth_client
object_type: Table
name: OAuth 2.0 client credentials table (t_oauth_client)
aliases: [t_oauth_client, adg.t_oauth_client]
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

# OAuth 2.0 client credentials table (t_oauth_client)

## 用途
物理表 `adg.t_oauth_client`,主键 `id`。OAuth 2.0 client credentials table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Auto-generated primary key · 可空 |
| `app_code` | varchar(31) | Client application code |
| `client_id` | varchar(63) | OAuth 2.0 client identifier |
| `client_secret` | varchar(255) | OAuth 2.0 client secret (encrypted) |
| `token_ttl_sec` | int | Access token time-to-live in seconds |
| `status` | tinyint | Client status: 1=active, 0=inactive |
| `created_at` | timestamp | Record creation timestamp · 可空 |
| `updated_at` | timestamp | Record last update timestamp · 可空 |

## 主键 / 索引
- 主键:`id`
- `client_id`:client_id (UNIQUE)
- `idx_app_code`:app_code
- `idx_client_id`:client_id

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
