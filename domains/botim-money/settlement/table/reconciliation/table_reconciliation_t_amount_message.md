---
id: tbl_reconciliation_t_amount_message
object_type: Table
name: 消息金额明细表 (t_amount_message)
aliases: [t_amount_message, reconciliation.t_amount_message]
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: reconciliation schema DDL
tags: [settlement, reconciliation]
sensitivity: normal
related_services: []
---

# 消息金额明细表 (t_amount_message)

## 用途
物理表 `reconciliation.t_amount_message`,主键 `id`。消息金额明细表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id 前八后九 |
| `message_type` | varchar(128) | 消息类型 |
| `bill_date` | char(8) | 对账日期 |
| `amount` | decimal(19, 4) | 金额 |
| `currency` | char(3) | 币种 |
| `memo` | varchar(255) | 备注 · 可空 |
| `extension` | varchar(255) | 扩展字段 · 可空 |
| `create_time` | timestamp | 创建时间 · 可空 |
| `update_time` | timestamp | 更新时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_billDate_messageType`:bill_date, message_type

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
