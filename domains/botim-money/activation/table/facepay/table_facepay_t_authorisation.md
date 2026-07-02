---
id: tbl_facepay_t_authorisation
object_type: Table
name: 支付授权表 (t_authorisation)
aliases: [t_authorisation, facepay.t_authorisation]
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

# 支付授权表 (t_authorisation)

## 用途
物理表 `facepay.t_authorisation`,主键 `id`。支付授权表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(18) | 主键 |
| `facial_data` | mediumtext | 面部数据 |
| `auth_amount` | decimal(15, 4) | 授权金额 · 可空 |
| `auth_type` | varchar(16) | 授权类型：Payment,OAuthLogin |
| `state` | varchar(32) | 授权状态：Init,FaceRecognised,PendingForAdditionalInfo,Authorized, |
| `unique_device` | varchar(64) | 设备唯一性标示 |
| `gmt_modified` | timestamp | 修改时间 · 可空 |
| `gmt_created` | timestamp | 创建时间 |
| `partner_id` | varchar(16) | 平台方id |
| `rm_judged` | varchar(2) | 是否风控判定过：Y:N |
| `rm_map` | varchar(1000) | 风控额外字段：json格式 |
| `addition_times` | int | 推进次数 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
