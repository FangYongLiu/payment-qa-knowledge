---
id: tbl_credit_t_cs_order_fund_route
object_type: Table
name: 放款渠道路由信息 (t_cs_order_fund_route)
aliases: [t_cs_order_fund_route, credit.t_cs_order_fund_route]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: credit schema DDL
tags: [lending, credit]
sensitivity: normal
related_services: []
---

# 放款渠道路由信息 (t_cs_order_fund_route)

## 用途
物理表 `credit.t_cs_order_fund_route`,主键 `id`。放款渠道路由信息。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 主键 · 可空 |
| `user_id` | varchar(50) | 用户ID |
| `order_no` | varchar(50) | 订单ID |
| `request_no` | varchar(50) | 流水号 |
| `vendor` | varchar(20) | 渠道号 |
| `status` | smallint(5) | 当前状态 |
| `finish_time` | timestamp | 完结时间 · 可空 |
| `created_time` | timestamp | 创建时间 · 可空 |
| `last_modified` | timestamp | 修改时间 · 可空 |
| `bank_card_id` | int | bank card table id · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_created_time`:created_time, status, vendor
- `idx_order_no`:order_no
- `idx_request_no`:request_no
- `idx_user_id`:user_id
- `idx_vendor`:vendor

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
