---
id: tbl_npss_t_oidc_token
object_type: Table
name: 授权token表 (t_oidc_token)
aliases: [t_oidc_token, npss.t_oidc_token]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: npss schema DDL
tags: [payment-core, npss]
sensitivity: normal
related_services: []
---

# 授权token表 (t_oidc_token)

## 用途
物理表 `npss.t_oidc_token`,主键 `id`。授权token表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(17) | token id |
| `user_id` | bigint(17) | 用户id |
| `token` | varchar(255) | 访问token |
| `id_token` | varchar(1024) | idToken · 可空 |
| `refresh_token` | varchar(64) | 刷新token |
| `token_type` | varchar(10) | token类型 · 可空 |
| `scope` | varchar(32) | 范围 · 可空 |
| `client_id` | varchar(32) | 客户端id |
| `status` | varchar(10) | 状态 |
| `auth_id` | bigint(17) | 授权id |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改时间 · 可空 |
| `gmt_expire` | timestamp | 过期时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- `uk_oidc_refresh_token`:refresh_token (UNIQUE)
- `uk_oidc_token`:token (UNIQUE)
- `idx_user_id_gmt_create`:user_id, gmt_create

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
