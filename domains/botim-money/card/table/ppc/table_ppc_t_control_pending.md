---
id: tbl_ppc_t_control_pending
object_type: Table
name: Control Pending (t_control_pending)
aliases: [t_control_pending, ppc.t_control_pending]
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

# Control Pending (t_control_pending)

## 用途
物理表 `ppc.t_control_pending`,主键 `trx_voucher_no`。Control Pending。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `trx_voucher_no` | bigint | Trx Voucher No |
| `pending_amount` | decimal(19, 4) | Pending Amount |
| `reversal_amount` | decimal(19, 4) | Reversal Amount · 可空 |
| `settle_amount` | decimal(19, 4) | Settle Amount |
| `settle_reversal_amount` | decimal(19, 4) | Settle Reversal Amount · 可空 |
| `extension` | varchar(255) | Extension · 可空 |
| `create_time` | timestamp | Create Time |
| `update_time` | timestamp | Update Time |

## 主键 / 索引
- 主键:`trx_voucher_no`
- `idx_update_time`:update_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
