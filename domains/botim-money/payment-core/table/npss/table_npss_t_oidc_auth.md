---
id: tbl_npss_t_oidc_auth
object_type: Table
name: 授权码唯一索引 (t_oidc_auth)
aliases: [t_oidc_auth, npss.t_oidc_auth]
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

# 授权码唯一索引 (t_oidc_auth)

## 用途
物理表 `npss.t_oidc_auth`,主键 `id`。授权码唯一索引。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(17) | 认证id · 可空 |
| `auth_code` | varchar(32) | 授权码 |
| `client_id` | varchar(32) | 客户端id |
| `user_id` | bigint(17) | 用户id · 可空 |
| `status` | varchar(10) | 状态 |
| `source` | char(5) | 来源， payby, aani · 可空 |
| `response_type` | varchar(32) | 响应类型 |
| `redirect_uri` | varchar(64) | 跳转url |
| `auth_state` | varchar(32) | 授权state码 · 可空 |
| `auth_nonce` | varchar(64) | 授权随机nonce · 可空 |
| `scope` | varchar(32) | 授权范围 |
| `extension` | varchar(512) | 扩展 · 可空 |
| `gmt_expired` | timestamp | 过期时间 · 可空 |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_auth_state`:auth_state
- `idx_oidc_auth_gmt`:gmt_create
- `idx_oidc_auth_user_id`:user_id

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
