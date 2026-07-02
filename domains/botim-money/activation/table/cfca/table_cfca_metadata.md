---
id: tbl_cfca_metadata
object_type: Table
name: metadata (metadata)
aliases: [metadata, cfca.metadata]
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

# metadata (metadata)

## 用途
物理表 `cfca.metadata`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(10) | 待补 · 可空 |
| `mobile_id` | bigint(10) | 待补 · 可空 |
| `aaid` | varchar(10) | 待补 |
| `upv` | varchar(255) | 待补 |
| `metadata_info` | varchar(20480) | 待补 · 可空 |
| `status` | bigint(1) | 待补 · 可空 |
| `remark` | varchar(255) | 待补 · 可空 |
| `auth_type` | varchar(20) | 待补 |
| `foreign` | key | 待补 · 可空 |

## 主键 / 索引
- 主键:`id`
- `IDX_METADATA_AAID`:aaid
- `IDX_METADATA_MOBILE_ID`:mobile_id

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
