---
id: tbl_promo_t_gw_unify_session
object_type: Table
name: OAuth login record (t_gw_unify_session)
aliases: [t_gw_unify_session, promo.t_gw_unify_session]
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

# OAuth login record (t_gw_unify_session)

## 用途
物理表 `promo.t_gw_unify_session`,主键 `id`。OAuth login record。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | ulid |
| `session_type` | char(10) | session type:OAuth |
| `provider` | char(10) | provider |
| `provider_uid` | varchar(32) | provider uid |
| `source_login_id` | varchar(32) | source login id |
| `source_token_id` | varchar(32) | source token id |
| `create_at` | timestamp | create at |
| `expire_at` | timestamp | expire at |
| `refresh_expire_at` | timestamp | refresh expire at |
| `update_at` | timestamp | update at |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
