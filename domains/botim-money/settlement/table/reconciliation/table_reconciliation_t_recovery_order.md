---
id: tbl_reconciliation_t_recovery_order
object_type: Table
name: RECOVERY ORDER (t_recovery_order)
aliases: [t_recovery_order, reconciliation.t_recovery_order]
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

# RECOVERY ORDER (t_recovery_order)

## 用途
物理表 `reconciliation.t_recovery_order`,主键 `request_no`。RECOVERY ORDER。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `request_no` | bigint | Request No |
| `member_id` | varchar(20) | Member Id |
| `recovery_amount` | decimal(19, 4) | Recovery Amount |
| `paid_amount` | decimal(19, 4) | Paid Amount |
| `currency` | char(3) | Currency |
| `credit_account_no` | varchar(32) | Credit Account No |
| `buiness_account` | varchar(32) | Buiness Account · 可空 |
| `status` | char | Status: I:Initial P:Pursuing S:Success F:Fail |
| `operator` | varchar(32) | Operator |
| `user_memo` | varchar(255) | User Memo · 可空 |
| `memo` | varchar(255) | Memo · 可空 |
| `extension` | varchar(255) | Extension · 可空 |
| `create_time` | timestamp | Create Time |
| `update_time` | timestamp | Update Time |

## 主键 / 索引
- 主键:`request_no`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
