---
id: tbl_promo_t_infr_bot_oauth_login
object_type: Table
name: bot oauth login for bot_vip (t_infr_bot_oauth_login)
aliases: [t_infr_bot_oauth_login, promo.t_infr_bot_oauth_login]
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

# bot oauth login for bot_vip (t_infr_bot_oauth_login)

## 用途
物理表 `promo.t_infr_bot_oauth_login`,主键 `id`。bot oauth login for bot_vip。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | ulid |
| `client_id` | varchar(100) | the client id of the bot |
| `access_token` | varchar(1024) | the access token of the bot |
| `refresh_token` | varchar(1024) | the refresh token of the bot · 可空 |
| `token_type` | varchar(20) | the token type of the bot |
| `expires_in` | int | the expires in of the bot |
| `scope` | varchar(200) | the scope of the bot |
| `jti` | varchar(50) | the jti of the bot |
| `uid` | varchar(32) | the uid of the bot · 可空 |
| `create_at` | timestamp | the create time of the bot oath login |
| `update_at` | timestamp | the update time of the bot oath login |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
