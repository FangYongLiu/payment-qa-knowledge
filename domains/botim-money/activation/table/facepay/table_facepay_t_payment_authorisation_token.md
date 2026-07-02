---
id: tbl_facepay_t_payment_authorisation_token
object_type: Table
name: 支付授权token (t_payment_authorisation_token)
aliases: [t_payment_authorisation_token, facepay.t_payment_authorisation_token]
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: facepay schema DDL
tags: [activation, facepay]
sensitivity: normal
related_services: []
---

# 支付授权token (t_payment_authorisation_token)

## 用途
物理表 `facepay.t_payment_authorisation_token`,主键 `id`。支付授权token。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(18) | 主键 |
| `authorisation_id` | bigint(18) | 支付授权表Id |
| `state` | varchar(32) | token状态 |
| `authorised_token` | varchar(64) | 授权token |
| `authorisation_token_ttl` | bigint(32) | 授权token过期时间 时间戳 |
| `member_id` | varchar(32) | 会员id |
| `member_shown` | varchar(20) | 会员展示信息 |
| `auth_amount` | decimal(15, 4) | 授权金额 · 可空 |
| `unique_device` | varchar(64) | 设备唯一标示 |
| `gmt_modified` | timestamp | 修改时间 · 可空 |
| `gmt_created` | timestamp | 创建时间 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
