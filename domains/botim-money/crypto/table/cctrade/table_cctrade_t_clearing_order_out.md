---
id: tbl_cctrade_t_clearing_order_out
object_type: Table
name: 清分输出 (t_clearing_order_out)
aliases: [t_clearing_order_out, cctrade.t_clearing_order_out]
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

# 清分输出 (t_clearing_order_out)

## 用途
物理表 `cctrade.t_clearing_order_out`,主键 `id`。清分输出。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id |
| `clearing_order_id` | bigint | 清分订单号 |
| `member_id` | varchar(32) | 会员ID |
| `refund_fee` | varchar(32) | 是否退费 |
| `principal_currency_code` | varchar(32) | 本金币种 |
| `principal_amount` | decimal(23, 8) | 本金金额 |
| `fee_currency_code` | varchar(32) | 费用币种 |
| `fee_amount` | decimal(23, 8) | 费用金额 |
| `total_currency_code` | varchar(32) | 总输出币种 |
| `total_amount` | decimal(23, 8) | 总输出金额 |
| `created_time` | timestamp(3) | 创建时间 |
| `last_updated_time` | timestamp(3) | 最后更新时间 |
| `data_version` | bigint | 数据版本 |

## 主键 / 索引
- 主键:`id`
- `uk_coo_tmid`:clearing_order_id, member_id (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
