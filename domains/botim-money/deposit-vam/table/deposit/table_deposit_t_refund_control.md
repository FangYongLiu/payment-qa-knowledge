---
id: tbl_deposit_t_refund_control
object_type: Table
name: Refund Control (t_refund_control)
aliases: [t_refund_control, deposit.t_refund_control]
domain: deposit-vam
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: deposit schema DDL
tags: [deposit-vam, deposit]
sensitivity: normal
related_services: []
---

# Refund Control (t_refund_control)

## 用途
物理表 `deposit.t_refund_control`,主键 `control_id`。Refund Control。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `control_id` | bigint | Control id: 17 digits, 8 date time digits + 9 sequence digits |
| `trade_voucher_no` | varchar(32) | Trade voucher number |
| `trade_amount` | decimal(19, 4) | Trade amount |
| `refundable_amount` | decimal(19, 4) | Refundable amount |
| `currency` | char(3) | Currency |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`control_id`
- `uk_trade_voucher_no`:trade_voucher_no (UNIQUE)
- `idx_update_time`:update_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
