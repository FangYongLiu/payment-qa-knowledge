---
id: tbl_appscore_t_points_trade
object_type: Table
name: 积分交易 (t_points_trade)
aliases: [t_points_trade, appscore.t_points_trade]
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

# 积分交易 (t_points_trade)

## 用途
物理表 `appscore.t_points_trade`,主键 `order_no`。积分交易。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `order_no` | varchar(50) | 订单号 |
| `points_trade_no` | bigint(18) | 积分交易号 · 可空 |
| `merchant_order_no` | varchar(64) | 外部商户订单号 |
| `status` | varchar(15) | 状态 |
| `gmt_create` | timestamp | 创建时间 · 可空 |
| `gmt_update` | timestamp | 主键 · 可空 |
| `payer_mid` | varchar(32) | 付款人 · 可空 |
| `payee_mid` | varchar(32) | 收款人 · 可空 |
| `payer_account_type` | varchar(32) | 付款人账户类型 · 可空 |
| `payee_account_type` | varchar(32) | 收款人账户类型 · 可空 |
| `points` | decimal(15, 2) | 积分 · 可空 |
| `biz_product_code` | varchar(15) | 业务产品码 · 可空 |

## 主键 / 索引
- 主键:`order_no`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
