---
id: tbl_ppc_t_transaction_monitor
object_type: Table
name: Transaction Monitor (t_transaction_monitor)
aliases: [t_transaction_monitor, ppc.t_transaction_monitor]
domain: card
status: active
owner: jianfei.wang
reviewer: jianfei.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ppc schema DDL
tags: [card, ppc]
sensitivity: normal
related_services: []
---

# Transaction Monitor (t_transaction_monitor)

## 用途
物理表 `ppc.t_transaction_monitor`,主键 `trx_voucher_no`。Transaction Monitor。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `trx_voucher_no` | bigint | Transaction Voucher Number |
| `member_id` | varchar(20) | Member ID |
| `debit_amount` | decimal(19, 4) | Debit Amount |
| `debit_currency` | char(3) | Debit Currency |
| `status` | char | Status: P-Processing;S-Success |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`trx_voucher_no`
- `idx_member_id`:member_id
- `idx_update_time`:update_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
