---
id: tbl_upic_t_transaction_control
object_type: Table
name: 记账控制 (t_transaction_control)
aliases: [t_transaction_control, upic.t_transaction_control]
domain: card
status: active
owner: jianfei.wang
reviewer: jianfei.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: upic schema DDL
tags: [card, upic]
sensitivity: normal
related_services: []
---

# 记账控制 (t_transaction_control)

## 用途
物理表 `upic.t_transaction_control`,主键 `control_id`。记账控制。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `control_id` | bigint | 控制id：前八后九 |
| `transaction_type` | varchar(10) | 记账类型：DEBIT=借记，CREDIT=贷记 |
| `trx_voucher_no` | bigint | 交易凭证 |
| `done_amount` | decimal(19, 4) | 已操作金额 |
| `undoable_amount` | decimal(19, 4) | 可反操作金额 |
| `currency_code` | char(3) | 币种 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`control_id`
- `uk_trx_voucher_no`:trx_voucher_no (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
