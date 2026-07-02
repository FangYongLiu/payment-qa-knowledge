---
id: tbl_npss_t_oidc_client
object_type: Table
name: 授权客户端表 (t_oidc_client)
aliases: [t_oidc_client, npss.t_oidc_client]
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

# 授权客户端表 (t_oidc_client)

## 用途
物理表 `npss.t_oidc_client`,主键 `id`。授权客户端表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 客户端id · 可空 |
| `client_id` | varchar(32) | 客户端名-唯一 |
| `client_secret` | varchar(255) | 客户端密码 · 可空 |
| `client_name` | varchar(64) | 客户端别名 · 可空 |
| `auth_method` | varchar(64) | 认证方式 · 可空 |
| `status` | char | A-可用，I-不可用 |
| `redirect_uris` | varchar(512) | 允许的跳转链接 |
| `response_types` | varchar(64) | 响应类型 |
| `grant_types` | varchar(255) | 允许的授权类型 |
| `scopes` | varchar(255) | 允许的范围 |
| `memo` | varchar(255) | 备注 · 可空 |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改时间 · 可空 |
| `extension` | varchar(255) | 扩展参数 · 可空 |

## 主键 / 索引
- 主键:`id`
- `uk_oidc_client_id`:client_id (UNIQUE)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
