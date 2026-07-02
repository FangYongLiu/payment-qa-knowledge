---
id: tbl_oauth_t_oauth_auth_info
object_type: Table
name: 鉴权信息。用于记录用户的鉴权记录（包括authcode, 生效时间，过期时间）。 (t_oauth_auth_info)
aliases: [t_oauth_auth_info, oauth.t_oauth_auth_info]
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: oauth schema DDL
tags: [activation, oauth]
sensitivity: normal
related_services: []
---

# 鉴权信息。用于记录用户的鉴权记录（包括authcode, 生效时间，过期时间）。 (t_oauth_auth_info)

## 用途
物理表 `oauth.t_oauth_auth_info`,主键 `id`。鉴权信息。用于记录用户的鉴权记录（包括authcode, 生效时间，过期时间）。。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | PK系统生成，数据的唯一标识 |
| `auth_code` | varchar(24) | 鉴权码 |
| `client_app_id` | bigint | 三方应用标识 |
| `user_id` | varchar(21) | 用户标识 |
| `auth_state` | varchar(64) | 鉴权状态 |
| `code_challenge` | varchar(256) | 鉴权码检验 |
| `code_challenge_method` | varchar(64) | 检验方法 |
| `scope` | varchar(100) | 范围 |
| `expire` | bigint | 过期时间 |
| `create_time` | bigint | 创建时间 |
| `update_time` | bigint | 更新时间 |
| `enable_flag` | varchar(2) | 可用标志。Y可用，或者其它代表“删除” |
| `status` | varchar(64) | 状态 |
| `response_type` | varchar(64) | 响应类型，code | token |

## 主键 / 索引
- 主键:`id`
- `i_oai_auth_code`:auth_code (UNIQUE)
- `i_oai_client_app_id`:client_app_id
- `i_oai_user_id_idx`:user_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
