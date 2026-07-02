---
id: tbl_cmf_t_return_order_channel_config
object_type: Table
name: return order no type config table (t_return_order_channel_config)
aliases: [t_return_order_channel_config, cmf.t_return_order_channel_config]
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

# return order no type config table (t_return_order_channel_config)

## 用途
物理表 `cmf.t_return_order_channel_config`,主键 `id`。return order no type config table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(10) | Primary key · 可空 |
| `channel_code` | varchar(32) | channel code |
| `return_no_type` | varchar(16) | return no type |
| `status` | char | status |
| `memo` | varchar(255) | Memo · 可空 |
| `gmt_create` | timestamp | Create time |
| `gmt_modified` | timestamp | Modified time |

## 主键 / 索引
- 主键:`id`
- `uk_trocc_channel_code`:channel_code (UNIQUE)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
