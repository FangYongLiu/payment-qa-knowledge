---
id: tbl_router_t_channel_batch_archive
object_type: Table
name: 批次管理表 (t_channel_batch_archive)
aliases: [t_channel_batch_archive, router.t_channel_batch_archive]
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

# 批次管理表 (t_channel_batch_archive)

## 用途
物理表 `router.t_channel_batch_archive`,主键 `archive_id`。批次管理表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `archive_id` | bigint(32) | 批次id |
| `api_code` | varchar(16) | 渠道api |
| `max_item` | smallint(10) | 最大笔数 |
| `order_no_rule_id` | bigint(32) | 订单号规则 · 可空 |
| `memo` | varchar(128) | 备注 · 可空 |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`archive_id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
