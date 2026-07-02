---
id: tbl_oauth_t_oauth_access_token
object_type: Table
name: 令牌信息。用于记录用户资源获取时所需要的token。 (t_oauth_access_token)
aliases: [t_oauth_access_token, oauth.t_oauth_access_token]
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

# 令牌信息。用于记录用户资源获取时所需要的token。 (t_oauth_access_token)

## 用途
物理表 `oauth.t_oauth_access_token`,主键 `id`。令牌信息。用于记录用户资源获取时所需要的token。。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | PK系统生成，数据的唯一标识 |
| `token_code` | varchar(64) | 令牌码 |
| `refresh_token_code` | varchar(64) | 令牌刷新码 |
| `old_token_id` | bigint | 被刷新时，旧的accessTokenId |
| `token_type` | varchar(64) | 令牌类型。取值：bearer |
| `scope` | varchar(255) | 范围 |
| `client_app_id` | bigint | 三方应用标识 |
| `user_id` | varchar(64) | 用户标识.ma的memberId |
| `authz_id` | bigint | 授权标识 |
| `create_time` | bigint | 创建时间 |
| `update_time` | bigint | 更新时间 |
| `expire` | bigint | 过期时间 |
| `status` | varchar(64) | 状态 |
| `enable_flag` | varchar(2) | 可用标志。Y可用，或者其它代表“删除” |

## 主键 / 索引
- 主键:`id`
- `i_oat_rtc`:refresh_token_code (UNIQUE)
- `i_oat_token_code`:token_code (UNIQUE)
- `i_oat_user_id_idx`:user_id, client_app_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
