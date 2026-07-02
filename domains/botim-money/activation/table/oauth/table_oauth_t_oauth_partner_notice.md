---
id: tbl_oauth_t_oauth_partner_notice
object_type: Table
name: 合作方通知 (t_oauth_partner_notice)
aliases: [t_oauth_partner_notice, oauth.t_oauth_partner_notice]
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

# 合作方通知 (t_oauth_partner_notice)

## 用途
物理表 `oauth.t_oauth_partner_notice`,主键 `id`。合作方通知。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | PK系统生成，数据的唯一标识 |
| `gather_id` | bigint | 关联t_oauth_gather_notice.id。 |
| `client_app_id` | bigint | 第三方应用标识 |
| `user_id` | varchar(32) | 用户标识，只记录单个用户，便于验证重复。 |
| `qty_classify` | varchar(32) | 全局收货地址变更为gsa，可多条一起通知。用户自定义收货地址的变更通知为usa，支持其它扩展。 |
| `notice_data` | varchar(2000) | 要通知的数据的json体。如果没有，就从数据中取，如果没有值，就从t_oauth_gather_notice中取。 |
| `data_id` | varchar(64) | 关联数据标识 |
| `has_notify` | varchar(2) | 已通知为Y，未通知为N，默认为N。 |
| `has_send_count` | int(4) | 用于记录重发时，发送了多少次。 |
| `create_time` | bigint | 创建时间 |
| `update_time` | bigint | 更新时间 |
| `status` | varchar(64) | 状态 |
| `enable_flag` | varchar(2) | 可用标志。Y可用，N或者其它代表“删除” |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
