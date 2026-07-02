---
id: tbl_eminstalment_t_channel_order
object_type: Table
name: 渠道交易订单表 (t_channel_order)
aliases: [t_channel_order, eminstalment.t_channel_order]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: eminstalment schema DDL
tags: [lending, eminstalment]
sensitivity: normal
related_services: []
---

# 渠道交易订单表 (t_channel_order)

## 用途
物理表 `eminstalment.t_channel_order`,主键 `id`。渠道交易订单表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 待补 · 可空 |
| `order_no` | varchar(64) | 渠道交易订单号，由payby生成并传入 |
| `payment_no` | bigint | 支付订单号 |
| `goods_order_no` | varchar(64) | 商品订单号 |
| `amount` | decimal(15, 2) | 要支付的金额 |
| `currency` | char(3) | 支付的货币 |
| `status` | smallint(4) | 待补 |
| `pay_time` | timestamp | 支付时间 · 可空 |
| `refund_time` | timestamp | 退款时间 · 可空 |
| `refund_order_no` | varchar(64) | 退款对应的渠道交易订单号 · 可空 |
| `create_time` | timestamp | 待补 |
| `update_time` | timestamp | 最后更新时间 |

## 主键 / 索引
- 主键:`id`
- `un_no`:order_no (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
