---
id: tbl_point_t_accounting_trade_control
object_type: Table
name: 记账交易控制 (t_accounting_trade_control)
aliases: [t_accounting_trade_control, point.t_accounting_trade_control]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: point schema DDL
tags: [marketing, point]
sensitivity: normal
related_services: []
---

# 记账交易控制 (t_accounting_trade_control)

## 用途
物理表 `point.t_accounting_trade_control`,主键 `trade_accounting_id`。记账交易控制。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `trade_accounting_id` | bigint | 交易记账id：18位，固定41+10位时间戳+4位序列+2位随机 |
| `account_no` | bigint | 账户号 |
| `point_type` | varchar(10) | 点数类型 |
| `frozen_amount` | decimal(19, 4) | 已冻结数量 |
| `unfrozen_amount` | decimal(19, 4) | 已解冻数量 |
| `paid_amount` | decimal(19, 4) | 已支出数量 |
| `refund_amount` | decimal(19, 4) | 已退回数量 |
| `extension` | varchar(255) | 扩展参数 · 可空 |
| `memo` | varchar(255) | 备注 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`trade_accounting_id`
- `idx_update_time_account_no`:update_time, account_no

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
