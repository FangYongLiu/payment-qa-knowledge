---
id: tbl_cmf_t_channel_field_mapping
object_type: Table
name: Channel field name mapping table (t_channel_field_mapping)
aliases: [t_channel_field_mapping, cmf.t_channel_field_mapping]
domain: payment-tool
status: active
owner: kingo.liang
reviewer: kingo.liang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: cmf schema DDL
tags: [payment-tool, cmf]
sensitivity: normal
related_services: []
---

# Channel field name mapping table (t_channel_field_mapping)

## 用途
物理表 `cmf.t_channel_field_mapping`,主键 `id`。Channel field name mapping table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(8) | primary key · 可空 |
| `channel_code` | varchar(16) | channel code |
| `source_field` | varchar(64) | source field name |
| `target_field` | varchar(64) | target field name |
| `status` | char | status: Y-enabled, N-disabled |
| `memo` | varchar(64) | description or notes · 可空 |
| `gmt_create` | timestamp(3) | creation time |
| `gmt_modified` | timestamp(3) | last modification time |

## 主键 / 索引
- 主键:`id`
- `uk_channel_source`:channel_code, source_field (UNIQUE)
- `ik_gmt_create`:gmt_create

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
