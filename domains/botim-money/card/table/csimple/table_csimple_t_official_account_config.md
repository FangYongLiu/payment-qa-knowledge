---
id: tbl_csimple_t_official_account_config
object_type: Table
name: Official Account OAuth Configuration (t_official_account_config)
aliases: [t_official_account_config, csimple.t_official_account_config]
domain: card
status: active
owner: jianfei.wang
reviewer: jianfei.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: csimple schema DDL
tags: [card, csimple]
sensitivity: normal
related_services: []
---

# Official Account OAuth Configuration (t_official_account_config)

## 用途
物理表 `csimple.t_official_account_config`,主键 `id`。Official Account OAuth Configuration。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key · 可空 |
| `partner_id` | varchar(32) | Platform partner ID (e.g. 200000000006) |
| `account_type` | varchar(32) | Official account business type (e.g. PAYBY, CASHNOW) |
| `oauth_key` | varchar(64) | OAuth identifier (e.g. PAYBY_OFFICIAL_ACCOUNTS) |
| `client_id` | varchar(128) | Botim OAuth2 client ID |
| `client_secret` | varchar(128) | Botim OAuth2 client secret |
| `oauth_mode` | varchar(32) | OAuth mode (CLIENT_CREDENTIALS / AUTHORIZATION_CODE) |
| `is_default` | char | Whether this is the default OA for the platform (Y/N) |
| `status` | char | Active status (Y/N) |
| `memo` | varchar(256) | Remarks · 可空 |
| `gmt_create` | datetime | Created time |
| `gmt_modified` | datetime | Last modified time |

## 主键 / 索引
- 主键:`id`
- `uk_partner_account_mode`:partner_id, account_type, oauth_mode (UNIQUE)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
