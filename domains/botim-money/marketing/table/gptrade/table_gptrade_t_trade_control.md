---
id: tbl_gptrade_t_trade_control
object_type: Table
name: 交易控制 (t_trade_control)
aliases: [t_trade_control, gptrade.t_trade_control]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: gptrade schema DDL
tags: [marketing, gptrade]
sensitivity: normal
related_services: []
---

# 交易控制 (t_trade_control)

## 用途
物理表 `gptrade.t_trade_control`,主键 `trade_voucher_no`。交易控制。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `trade_voucher_no` | bigint | 交易凭证号：18位，固定14+10位时间戳+4位序列+2位随机 |
| `processable_amount` | decimal(19, 4) | 可处理金额 |
| `processing_amount` | decimal(19, 4) | 处理中金额 |
| `settled_amount` | decimal(19, 4) | 已结算金额 |
| `cancelled_amount` | decimal(19, 4) | 已撤销金额 |
| `refundable_amount` | decimal(19, 4) | 可退款金额 |
| `refunding_amount` | decimal(19, 4) | 退款中金额 |
| `refunded_amount` | decimal(19, 4) | 已退款金额 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`trade_voucher_no`
- `idx_update_time`:update_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
