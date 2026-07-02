---
id: tbl_eminstalment_t_trade_order
object_type: Table
name: 分期支付中信贷相关的与账相关的交易订单表 (t_trade_order)
aliases: [t_trade_order, eminstalment.t_trade_order]
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

# 分期支付中信贷相关的与账相关的交易订单表 (t_trade_order)

## 用途
物理表 `eminstalment.t_trade_order`,主键 `id`。分期支付中信贷相关的与账相关的交易订单表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int(11) | 待补 · 可空 |
| `order_no` | varchar(64) | 自己生成的交易订单号 |
| `instalment_order_no` | varchar(64) | 分期支付订单no,对应t_instalment_order表的order_no |
| `trade_type` | smallint | 待补 · 可空 |
| `amount` | decimal(15, 2) | 支付金额 |
| `finish_time` | timestamp | 交易完成时间 · 可空 |
| `status` | smallint | 状态 0 待提交，1，已提交， 2 交易（支付）成功 ，-2 交易（支付）失败 ，3 订单关闭（主要是有payment的trade_type时，payment过期) |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 修改时间 |
| `related_trade_id` | int | 当交易是退**相关的时记录被退的交易的订单号 · 可空 |
| `currency` | char(3) | 待补 |
| `payment_no` | bigint | 对于涉及支付的交易，关联的是支付的订单id（对应payment_record的payment_no） · 可空 |
| `payment_way` | smallint(4) | 支付方式:1、线上支付，2、线下支付 · 可空 |
| `payment_time` | timestamp | 支付入帐时间,线下支付是凭证上的时间，线上支付时是payby给出回调的时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- `uk_on`:order_no (UNIQUE)
- `uk_pn`:payment_no (UNIQUE)
- `idx_ion`:instalment_order_no

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
