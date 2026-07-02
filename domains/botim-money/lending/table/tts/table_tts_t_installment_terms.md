---
id: tbl_tts_t_installment_terms
object_type: Table
name: Installment terms (t_installment_terms)
aliases: [t_installment_terms, tts.t_installment_terms]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: tts schema DDL
tags: [lending, tts]
sensitivity: normal
related_services: []
---

# Installment terms (t_installment_terms)

## 用途
物理表 `tts.t_installment_terms`,主键 `terms_id`。Installment terms。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `terms_id` | bigint(21) | terms id · 可空 |
| `supplier_code` | varchar(5) | supplier: VISA/ |
| `terms_version` | varchar(50) | terms version |
| `seq_no` | smallint(10) | seq_no, from 0 to 9999 |
| `content` | varchar(512) | content |
| `gmt_create` | timestamp(3) | create time |

## 主键 / 索引
- 主键:`terms_id`
- `uk_installment_terms`:supplier_code, terms_version, seq_no (UNIQUE)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
