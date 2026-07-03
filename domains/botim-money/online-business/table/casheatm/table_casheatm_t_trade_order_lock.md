---
id: tbl_casheatm_t_trade_order_lock
object_type: Table
name: topup订单锁 (t_trade_order_lock)
aliases: [t_trade_order_lock, casheatm.t_trade_order_lock]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: casheatm schema DDL
tags: [online-business, casheatm]
sensitivity: normal
related_services: [svc_cash_eatm]
---

# topup订单锁 (t_trade_order_lock)

## 用途
物理表 `casheatm.t_trade_order_lock`,主键 `device_id, trade_order_id`。topup订单锁。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `device_id` | bigint | 设备id |
| `trade_order_id` | bigint | 交易订单号 |

## 主键 / 索引
- 主键:`device_id, trade_order_id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
