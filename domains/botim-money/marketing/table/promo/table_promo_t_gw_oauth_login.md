---
id: tbl_promo_t_gw_oauth_login
object_type: Table
name: OAuth login record (t_gw_oauth_login)
aliases: [t_gw_oauth_login, promo.t_gw_oauth_login]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: promo schema DDL
tags: [marketing, promo]
sensitivity: normal
related_services: []
---

# OAuth login record (t_gw_oauth_login)

## 用途
物理表 `promo.t_gw_oauth_login`,主键 `id`。OAuth login record。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | ulid |
| `provider` | char(10) | provider |
| `grant_type` | varchar(20) | grant type:AuthorizationCode|PKCE|ClientCredentials|DeviceCode|RefreshToken |
| `redirect_uri` | varchar(255) | redirect uri |
| `auth_code` | varchar(64) | auth code |
| `status` | varchar(20) | status:Created|ProviderPassed|ProviderRejected|ProviderFailed|Failed |
| `create_at` | timestamp | create at |
| `update_at` | timestamp | update at |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
