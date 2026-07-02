---
id: tbl_router_t_channel_ext
object_type: Table
name: 渠道扩展表 (t_channel_ext)
aliases: [t_channel_ext, router.t_channel_ext]
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

# 渠道扩展表 (t_channel_ext)

## 用途
物理表 `router.t_channel_ext`,主键 `ext_id`。渠道扩展表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `ext_id` | int(32) | 扩展id · 可空 |
| `channel_code` | varchar(32) | 渠道编号 |
| `attr_key` | varchar(32) | 扩展key · 可空 |
| `attr_value` | varchar(500) | 扩展值 · 可空 |
| `need_match` | char | 需要匹配 · 可空 |
| `match_type` | varchar(10) | 匹配类型 |
| `extension` | varchar(32) | 扩展 · 可空 |
| `gmt_create` | timestamp | 创建时间 · 可空 |
| `gmt_modified` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`ext_id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
