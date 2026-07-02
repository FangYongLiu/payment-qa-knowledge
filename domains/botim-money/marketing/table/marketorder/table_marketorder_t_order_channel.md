---
id: tbl_marketorder_t_order_channel
object_type: Table
name: 订单渠道信息表 (t_order_channel)
aliases: [t_order_channel, marketorder.t_order_channel]
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

# 订单渠道信息表 (t_order_channel)

## 用途
物理表 `marketorder.t_order_channel`,主键 `id`。订单渠道信息表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(18) | 主键 · 可空 |
| `order_no` | bigint(18) | 订单号 |
| `supplier_order_no` | varchar(32) | 供应商订单号 · 可空 |
| `channel_order_no` | varchar(32) | 渠道订单号 · 可空 |
| `channel_code` | varchar(32) | 渠道编号 · 可空 |
| `supplier_merchant_id` | varchar(32) | 供应商商户ID · 可空 |
| `supplier_merchant_uid` | varchar(32) | 供应商商户UID · 可空 |
| `supplier_acc_type` | varchar(12) | 供应商账户类型 · 可空 |
| `supplier_acc_no` | varchar(64) | 供应商账号 · 可空 |
| `supplier_no` | varchar(64) | 供应商编号 · 可空 |
| `channel_cost` | decimal(15, 4) | 渠道成本 · 可空 |
| `channel_profit` | decimal(15, 4) | 渠道利润 · 可空 |
| `currency` | varchar(10) | 币种 · 可空 |
| `gmt_created` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- `IDX_ORDER_NO`:order_no

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
