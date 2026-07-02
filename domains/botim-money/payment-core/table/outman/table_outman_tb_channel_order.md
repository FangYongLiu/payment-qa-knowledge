---
id: tbl_outman_tb_channel_order
object_type: Table
name: 渠道订单表 (tb_channel_order)
aliases: [tb_channel_order, outman.tb_channel_order]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: outman schema DDL
tags: [payment-core, outman]
sensitivity: normal
related_services: []
---

# 渠道订单表 (tb_channel_order)

## 用途
物理表 `outman.tb_channel_order`,主键 `channel_order_id`。渠道订单表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `channel_order_id` | bigint(32) | id |
| `request_id` | varchar(32) | 前置系统订单号 |
| `member_id` | varchar(32) | 会员编号 · 可空 |
| `biz_type` | varchar(32) | 订单类型 |
| `channel_code` | varchar(32) | 渠道编号 |
| `status` | varchar(16) | 认证结果 |
| `resp_code` | varchar(16) | outMan响应码 |
| `resp_msg` | varchar(128) | outMan响应描述 · 可空 |
| `channel_resp_code` | varchar(32) | 渠道响应码 · 可空 |
| `channel_resp_msg` | varchar(256) | 渠道响应描述 · 可空 |
| `event_type` | varchar(32) | 业务事件类型，业务方自定义 · 可空 |
| `gmt_create` | timestamp | 订单创建时间 |
| `gmt_modified` | timestamp | 订单更新时间 · 可空 |
| `request_data` | varchar(1024) | 请求详情 · 可空 |
| `response_data` | varchar(2000) | channel response · 可空 |
| `client_id` | varchar(32) | 应用ID · 可空 |
| `extension` | varchar(1024) | 拓展信息 · 可空 |
| `journey_order_id` | bigint | Journey order id · 可空 |

## 主键 / 索引
- 主键:`channel_order_id`
- `idx_gmt_create`:gmt_create
- `idx_journey_order_id`:journey_order_id
- `idx_member_id`:member_id

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
