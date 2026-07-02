---
id: tbl_marketorder_t_order_config
object_type: Table
name: 订单配置表 (t_order_config)
aliases: [t_order_config, marketorder.t_order_config]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: marketorder schema DDL
tags: [marketing, marketorder]
sensitivity: normal
related_services: []
---

# 订单配置表 (t_order_config)

## 用途
物理表 `marketorder.t_order_config`,主键 `id`。订单配置表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 主键 · 可空 |
| `order_type` | varchar(3) | 1:普通订单 2:话费订单 3:流量订单 4:SALIK订单 5:水电费订单 6:停车充值订单 7:停车缴罚单费订单 |
| `biz_product_code` | varchar(12) | 250501:话费充值,250502流量充值 250201:salik充值 250101:水电费 250401:停车充值 250402:停车缴费 · 可空 |
| `merchant_id` | varchar(32) | 商户id · 可空 |
| `merchant_uid` | varchar(32) | 商户uid · 可空 |
| `profit_merchant_id` | varchar(32) | 利润商户id · 可空 |
| `profit_merchant_uid` | varchar(32) | 利润商户uid · 可空 |
| `profit_account_no` | varchar(32) | 利润账户号 · 可空 |
| `profit_account_type` | varchar(16) | 利润账户类型 · 可空 |
| `market_account_no` | varchar(32) | 营销账户号 · 可空 |
| `gmt_created` | timestamp | 创建时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
