---
id: tbl_tts_t_installment_supplier
object_type: Table
name: Installment supplier (t_installment_supplier)
aliases: [t_installment_supplier, tts.t_installment_supplier]
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

# Installment supplier (t_installment_supplier)

## 用途
物理表 `tts.t_installment_supplier`,主键 `supplier_code`。Installment supplier。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `supplier_code` | varchar(10) | supplier_code;supplier code, VISA/ |
| `supplier_name` | varchar(32) | supplier_name;supplier name · 可空 |
| `status` | char | status,A-Available,U-Unavailable · 可空 |
| `gmt_create` | timestamp(3) | create time · 可空 |
| `gmt_modified` | timestamp(3) | modify time · 可空 |
| `memo` | varchar(64) | memo · 可空 |

## 主键 / 索引
- 主键:`supplier_code`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
