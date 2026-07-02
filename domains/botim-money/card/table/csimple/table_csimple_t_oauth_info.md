---
id: tbl_csimple_t_oauth_info
object_type: Table
name: 授权信息表 (t_oauth_info)
aliases: [t_oauth_info, csimple.t_oauth_info]
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

# 授权信息表 (t_oauth_info)

## 用途
物理表 `csimple.t_oauth_info`,主键 `oauth_id`。授权信息表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `oauth_id` | bigint(17) | 主键 |
| `partner_id` | varchar(32) | 平台ID |
| `uid` | varchar(32) | 用户uid |
| `access_token_type` | varchar(20) | token 类型 |
| `access_token` | varchar(4000) | token |
| `expired_time` | timestamp | 过期时间 |
| `refresh_token` | varchar(4000) | 刷新token · 可空 |
| `scope` | varchar(200) | 授权scope · 可空 |
| `status` | tinyint | 状态（0 - 正常,1 - 过期,3 - 用户在第三方不存在） |
| `client_id` | varchar(50) | OAuth2授权，clint id |
| `gmt_created` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`oauth_id`
- `uk_oh_info_pid_u_c`:partner_id, uid, client_id, oauth_id (UNIQUE)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
