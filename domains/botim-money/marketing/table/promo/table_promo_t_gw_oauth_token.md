---
id: tbl_promo_t_gw_oauth_token
object_type: Table
name: OAuth login record (t_gw_oauth_token)
aliases: [t_gw_oauth_token, promo.t_gw_oauth_token]
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

# OAuth login record (t_gw_oauth_token)

## 用途
物理表 `promo.t_gw_oauth_token`,主键 `id`。OAuth login record。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | ulid |
| `login_id` | varchar(32) | login id |
| `provider` | char(10) | provider |
| `access_token` | varchar(1024) | access token |
| `refresh_token` | varchar(1024) | refresh token |
| `token_type` | varchar(50) | token type |
| `expires_in` | bigint | expires in |
| `scope` | varchar(255) | scope |
| `jti` | varchar(255) | jti |
| `uid` | varchar(64) | uid |
| `create_at` | timestamp | create at |
| `update_at` | timestamp | update at |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
