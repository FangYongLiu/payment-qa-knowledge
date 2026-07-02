---
id: tbl_reconciliation_t_balance_record
object_type: Table
name: 余额记录 (t_balance_record)
aliases: [t_balance_record, reconciliation.t_balance_record]
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

# 余额记录 (t_balance_record)

## 用途
物理表 `reconciliation.t_balance_record`,主键 `flow_id`。余额记录。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `flow_id` | bigint(17) | 主键ID |
| `bank_code` | varchar(8) | 银行编号 · 可空 |
| `bill_date` | date | 对账日期 · 可空 |
| `bank_amount` | decimal(15, 2) | 银行余额 · 可空 |
| `account_amount` | decimal(15, 2) | 账户余额 · 可空 |
| `currency` | varchar(3) | 币种 · 可空 |
| `memo` | varchar(255) | 备注 · 可空 |
| `gmt_create` | timestamp | 创建时间 · 可空 |
| `gmt_modified` | timestamp | 更新时间 · 可空 |

## 主键 / 索引
- 主键:`flow_id`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
