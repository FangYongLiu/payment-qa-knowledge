---
id: tbl_cmf_t_channel_code_mapping
object_type: Table
name: Channel code mapping rule table (t_channel_code_mapping)
aliases: [t_channel_code_mapping, cmf.t_channel_code_mapping]
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

# Channel code mapping rule table (t_channel_code_mapping)

## 用途
物理表 `cmf.t_channel_code_mapping`,主键 `id`。Channel code mapping rule table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(10) | Primary key · 可空 |
| `rule_name` | varchar(64) | Rule name |
| `old_channel_code` | varchar(32) | Original channel code |
| `new_channel_code` | varchar(32) | New channel code |
| `match_expression` | varchar(1024) | Match expression · 可空 |
| `priority` | mediumint(4) | Priority (higher number means higher priority) |
| `status` | char | Status: Y-enabled, N-disabled · 可空 |
| `memo` | varchar(255) | Memo · 可空 |
| `gmt_create` | timestamp | Create time |
| `gmt_modified` | timestamp | Modified time |

## 主键 / 索引
- 主键:`id`
- `uk_tccp_onp`:old_channel_code, new_channel_code, priority (UNIQUE)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
