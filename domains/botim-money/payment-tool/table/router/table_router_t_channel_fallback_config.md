---
id: tbl_router_t_channel_fallback_config
object_type: Table
name: fallback channel configuration table (t_channel_fallback_config)
aliases: [t_channel_fallback_config, router.t_channel_fallback_config]
domain: payment-tool
status: active
owner: kingo.liang
reviewer: kingo.liang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: router schema DDL
tags: [payment-tool, router]
sensitivity: normal
related_services: []
---

# fallback channel configuration table (t_channel_fallback_config)

## 用途
物理表 `router.t_channel_fallback_config`,主键 `id`。fallback channel configuration table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(8) | primary key · 可空 |
| `merchant_id` | varchar(16) | Merchant ID |
| `channel_code_list` | varchar(128) | Channel code list, comma separated |
| `enabled` | char | Is enabled,Y/N |
| `priority` | int | Configuration priority · 可空 |
| `memo` | varchar(255) | Memo · 可空 |
| `gmt_create` | timestamp | Create time |
| `gmt_modified` | timestamp | Modified time |

## 主键 / 索引
- 主键:`id`
- `ik_gmt_create`:gmt_create
- `ik_merchant_id`:merchant_id

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
