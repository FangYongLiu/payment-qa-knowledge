---
id: tbl_router_t_channel_api
object_type: Table
name: 渠道接口表 (t_channel_api)
aliases: [t_channel_api, router.t_channel_api]
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

# 渠道接口表 (t_channel_api)

## 用途
物理表 `router.t_channel_api`,主键 `api_code`。渠道接口表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `api_code` | varchar(32) | 接口编号 |
| `channel_code` | varchar(32) | 渠道编号 · 可空 |
| `api_type` | varchar(32) | 接口类型 · 可空 |
| `api_method` | varchar(10) | dubbo-dubbo服务, ws-webservice，method-本地方法 · 可空 |
| `api_url` | varchar(256) | 接口地址 · 可空 |
| `order_no_rule_id` | bigint(32) | 订单号规则 · 可空 |
| `api_priority` | int(10) | 接口优先级 · 可空 |
| `status` | char | 状态， · 可空 |
| `gmt_create` | timestamp | 创建时间 · 可空 |
| `gmt_modified` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`api_code`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
