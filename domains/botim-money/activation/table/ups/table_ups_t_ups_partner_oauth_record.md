---
id: tbl_ups_t_ups_partner_oauth_record
object_type: Table
name: 用途：第三方授权记录.只记录用户的授权及授权后的用户ID,不做绑定. (t_ups_partner_oauth_record)
aliases: [t_ups_partner_oauth_record, ups.t_ups_partner_oauth_record]
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ups schema DDL
tags: [activation, ups]
sensitivity: normal
related_services: []
---

# 用途：第三方授权记录.只记录用户的授权及授权后的用户ID,不做绑定. (t_ups_partner_oauth_record)

## 用途
物理表 `ups.t_ups_partner_oauth_record`,主键 `id`。用途：第三方授权记录.只记录用户的授权及授权后的用户ID,不做绑定.。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | PK系统生成，数据的唯一标识. |
| `partner_oauth_id` | varchar(64) | 即t_ups_partner_oauth.id · 可空 |
| `partner_mark` | varchar(64) | 分twitter,totok · 可空 |
| `auth_code` | varchar(512) | 授权码 · 可空 |
| `access_token` | varchar(1024) | 访问令牌 · 可空 |
| `refresh_token` | varchar(1024) | 刷新访问令牌 · 可空 |
| `id_token` | varchar(2000) | 授权信息 · 可空 |
| `partner_uid` | varchar(64) | 第三方用户ID · 可空 |
| `partner_account` | varchar(64) | 第三方用户账户 · 可空 |
| `data_remark` | varchar(255) | 数据备注 · 可空 |
| `bind_status` | varchar(64) | 绑定状态.绑定成功为bound,绑定中为binding,注删成功后为bound · 可空 |
| `create_time` | bigint | 创建时间 · 可空 |
| `update_time` | bigint | 更新时间 · 可空 |
| `enable_flag` | varchar(2) | 可用标志。Y可用，或者其它代表“删除” · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
