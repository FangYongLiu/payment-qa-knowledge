---
id: tbl_cctrade_t_payment_control
object_type: Table
name: 交易订单 (t_payment_control)
aliases: [t_payment_control, cctrade.t_payment_control]
domain: crypto
status: active
owner: can.wang
reviewer: can.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: cctrade schema DDL
tags: [crypto, cctrade]
sensitivity: normal
related_services: []
---

# 交易订单 (t_payment_control)

## 用途
物理表 `cctrade.t_payment_control`,主键 `id`。交易订单。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id |
| `payer_mid` | varchar(32) | 付款人mid · 可空 |
| `decision` | varchar(32) | 决定 · 可空 |
| `binded_payment_order_id` | bigint | 被选择的支付订单 · 可空 |
| `created_time` | timestamp(3) | 创建时间 |
| `last_updated_time` | timestamp(3) | 最后更新时间 |
| `data_version` | bigint | 数据版本 |

## 主键 / 索引
- 主键:`id`
- `i_to_ct`:created_time
- `i_to_lut`:last_updated_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
