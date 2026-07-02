---
id: tbl_installmentcard_t_ic_doc_document_record
object_type: Table
name: Installment card document generation records (t_ic_doc_document_record)
aliases: [t_ic_doc_document_record, installmentcard.t_ic_doc_document_record]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: installmentcard schema DDL
tags: [lending, installmentcard]
sensitivity: normal
related_services: []
---

# Installment card document generation records (t_ic_doc_document_record)

## 用途
物理表 `installmentcard.t_ic_doc_document_record`,主键 `id`。Installment card document generation records。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 待补 · 可空 |
| `member_id` | varchar(64) | Member ID |
| `reference_no` | varchar(64) | Reference number (application no, billing period, etc.) |
| `document_type` | tinyint | 0=CREDIT_AGREEMENT, 1=DIRECT_DEBIT_AGREEMENT, 2=KEY_FACTS_STATEMENT, 3=MONTHLY_STATEMENT |
| `file_tag` | varchar(128) | File storage key / tag after upload · 可空 |
| `created_at` | datetime(3) | Record creation time |
| `updated_at` | datetime(3) | Last update time |

## 主键 / 索引
- 主键:`id`
- `uk_member_ref_type`:member_id, reference_no (UNIQUE)
- `idx_member_id`:member_id

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
