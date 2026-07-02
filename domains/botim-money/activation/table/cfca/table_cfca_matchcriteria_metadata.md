---
id: tbl_cfca_matchcriteria_metadata
object_type: Table
name: matchcriteria_metadata (matchcriteria_metadata)
aliases: [matchcriteria_metadata, cfca.matchcriteria_metadata]
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: cfca schema DDL
tags: [activation, cfca]
sensitivity: normal
related_services: []
---

# matchcriteria_metadata (matchcriteria_metadata)

## 用途
物理表 `cfca.matchcriteria_metadata`,主键 `matchcriteria_id, metadata_id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `matchcriteria_id` | bigint(11) | 待补 |
| `metadata_id` | bigint(11) | 待补 |
| `type` | bigint(1) | 待补 |
| `user_verify` | bigint(11) | 待补 |
| `foreign` | key | 待补 · 可空 |
| `on` | update | 待补 · 可空 |
| `foreign` | key | 待补 · 可空 |
| `on` | update | 待补 · 可空 |

## 主键 / 索引
- 主键:`matchcriteria_id, metadata_id`
- `IDX_MM_MATCHCRITERIA_ID`:matchcriteria_id
- `IDX_MM_METADATA_METADATA_ID`:metadata_id

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
