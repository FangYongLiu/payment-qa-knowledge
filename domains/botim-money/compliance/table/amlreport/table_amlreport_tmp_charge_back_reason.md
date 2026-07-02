---
id: tbl_amlreport_tmp_charge_back_reason
object_type: Table
name: tmp_charge_back_reason (tmp_charge_back_reason)
aliases: [tmp_charge_back_reason, amlreport.tmp_charge_back_reason]
domain: compliance
status: active
owner: dewen.li
reviewer: dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: amlreport schema DDL
tags: [compliance, amlreport]
sensitivity: normal
related_services: []
---

# tmp_charge_back_reason (tmp_charge_back_reason)

## 用途
物理表 `amlreport.tmp_charge_back_reason`,主键 `None`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `inst_order_no` | varchar(20) | inst order no · 可空 |
| `merchant_id` | varchar(20) | merchant id · 可空 |
| `amount` | decimal(10, 2) | amount · 可空 |
| `dispute_date` | timestamp | dispute date · 可空 |
| `update_date` | timestamp | update date · 可空 |
| `status` | varchar(50) | status · 可空 |
| `rc` | varchar(100) | rc · 可空 |

## 主键 / 索引
- 主键:`None`
- `inst_order_no`:inst_order_no

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
