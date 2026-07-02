---
id: tbl_oauth_t_oauth_client_app
object_type: Table
name: 第三方App信息表 (t_oauth_client_app)
aliases: [t_oauth_client_app, oauth.t_oauth_client_app]
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

# 第三方App信息表 (t_oauth_client_app)

## 用途
物理表 `oauth.t_oauth_client_app`,主键 `id`。第三方App信息表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 待补 |
| `client_id` | varchar(32) | 第三方应用编号 |
| `client_secret` | varchar(64) | 第三方应用密钥 |
| `logo` | varchar(255) | 第三方应用Logo URL |
| `provider` | varchar(100) | 第三方应用提供商名称 |
| `redirect_url` | varchar(256) | 跳转url |
| `description` | varchar(2000) | 第三方应用描述 |
| `status` | varchar(10) | 状态：active | inactive |
| `sort` | int unsigned | 排序 |
| `weight` | int(21) | 显示权重。1显示到手机SDK，0不显示 |
| `scopes` | varchar(255) | 应用需要的scope范围，多个用空格拆分 |
| `name` | varchar(255) | 应用名称 |
| `accept_sa_notify` | varchar(255) | 应用接受收货地址修改消息。接受为Y，否则为N。 |
| `address_notify_url` | varchar(1000) | 收货地址修改回调网址 · 可空 |
| `cooperation_mode` | varchar(64) | 合作模式 |
| `partner_id` | varchar(64) | 合作方标识 |
| `create_time` | bigint | 创建时间 |
| `update_time` | bigint | 更新时间 |
| `enable_flag` | varchar(2) | 可用标志。Y可用，或者其它代表”删除“ |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
