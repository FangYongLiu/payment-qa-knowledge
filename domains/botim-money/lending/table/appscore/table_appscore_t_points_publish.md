---
id: tbl_appscore_t_points_publish
object_type: Table
name: 积分发行 (t_points_publish)
aliases: [t_points_publish, appscore.t_points_publish]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: appscore schema DDL
tags: [lending, appscore]
sensitivity: normal
related_services: []
---

# 积分发行 (t_points_publish)

## 用途
物理表 `appscore.t_points_publish`,主键 `publish_points_no`。积分发行。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `publish_points_no` | bigint(18) | 主键 |
| `merchant_order_no` | varchar(64) | 商户订单号 |
| `order_no` | varchar(50) | 订单号 |
| `biz_product_code` | varchar(15) | 产品码 |
| `payer_mid` | varchar(32) | 付款人 · 可空 |
| `payee_mid` | varchar(32) | 收款人 · 可空 |
| `points` | decimal(15, 2) | 积分数量 · 可空 |
| `amount` | decimal(15, 2) | 金额 |
| `status` | varchar(15) | 状态 |
| `request_time` | timestamp | 请求时间 |
| `notify_url` | varchar(255) | 通知地址 · 可空 |
| `accessory_content` | varchar(700) | 附属内容 · 可空 |
| `fail_code` | varchar(20) | 错误编码 · 可空 |
| `gmt_create` | timestamp | 创建时间 · 可空 |
| `gmt_modify` | timestamp | 修改时间 · 可空 |
| `summary` | varchar(255) | 备注 · 可空 |
| `partner_id` | varchar(32) | 商户号 · 可空 |
| `merchant_account_type` | varchar(32) | 商户账户类型 · 可空 |

## 主键 / 索引
- 主键:`publish_points_no`
- `uk_index_order_no`:order_no (UNIQUE)
- `uk_index_gmt_update`:gmt_modify

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
