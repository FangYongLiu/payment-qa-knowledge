---
id: tbl_ups_t_ups_partner_oauth
object_type: Table
name: 用途：第三方授权.合作方(例如totok,twitter,hms)用户通过在其它平台授权来登录到ups的授权数据。授权完了,要绑定一个手机号. (t_ups_partner_oauth)
aliases: [t_ups_partner_oauth, ups.t_ups_partner_oauth]
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

# 用途：第三方授权.合作方(例如totok,twitter,hms)用户通过在其它平台授权来登录到ups的授权数据。授权完了,要绑定一个手机号. (t_ups_partner_oauth)

## 用途
物理表 `ups.t_ups_partner_oauth`,主键 `id`。用途：第三方授权.合作方(例如totok,twitter,hms)用户通过在其它平台授权来登录到ups的授权数据。授权完了,要绑定一个手机号.。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | PK系统生成，数据的唯一标识. |
| `mid` | varchar(64) | 即ma的memberId · 可空 |
| `uid` | varchar(64) | 冗余字段.依赖t_ups_register_record.id · 可空 |
| `partner_uid` | varchar(255) | 合作方(比如hms的用户id) · 可空 |
| `mobile_number` | varchar(64) | 授权时绑定的手机号.冗余 · 可空 |
| `email` | varchar(64) | 邮箱.第三方的邮箱 · 可空 |
| `auth_type` | varchar(64) | 分oauth1,oauth2 · 可空 |
| `partner_mark` | varchar(64) | 分twitter,totok · 可空 |
| `authenticity_token` | varchar(64) | 认证token,只有oauth1才有值 · 可空 |
| `call_back_confirm` | varchar(4) | 需要确认为Y · 可空 |
| `oauth_verifier` | varchar(64) | 授权验证,只有oauth1才有值 · 可空 |
| `oauth_token` | varchar(255) | 授权token,一般oauth1才有 · 可空 |
| `oauth_token_secret` | varchar(64) | 授权secret,只有oauth1才有值 · 可空 |
| `access_token` | varchar(1024) | 访问令牌 · 可空 |
| `access_token_secret` | varchar(64) | 访问secret,只有oauth1才有值 · 可空 |
| `refresh_token` | varchar(1024) | 刷新令牌 · 可空 |
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
