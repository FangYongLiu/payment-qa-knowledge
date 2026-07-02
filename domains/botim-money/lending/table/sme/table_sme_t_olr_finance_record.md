---
id: tbl_sme_t_olr_finance_record
object_type: Table
name: Serial number index (t_olr_finance_record)
aliases: [t_olr_finance_record, sme.t_olr_finance_record]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: sme schema DDL
tags: [lending, sme]
sensitivity: normal
related_services: []
---

# Serial number index (t_olr_finance_record)

## 用途
物理表 `sme.t_olr_finance_record`,主键 `id`。Serial number index。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(10) | 待补 · 可空 |
| `reference_no` | varchar(50) | Serial number |
| `transaction_time` | date | Trading hours |
| `deposit_details` | varchar(120) | Transaction description |
| `amount` | decimal(10, 2) | amount |
| `currency` | char(3) | Monetary unit |
| `sender_bank_code` | varchar(50) | Remitting bank code |
| `remitter_info` | varchar(50) | 汇款银行代码 |
| `status` | smallint | 待补 |
| `create_time` | timestamp | Creation time |
| `update_time` | timestamp | Modification time |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
