---
id: tbl_gpoint_t_accept_order
object_type: Table
name: 承兑订单 (t_accept_order)
aliases: [t_accept_order, gpoint.t_accept_order]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: gpoint schema DDL
tags: [marketing, gpoint]
sensitivity: normal
related_services: []
---

# 承兑订单 (t_accept_order)

## 用途
物理表 `gpoint.t_accept_order`,主键 `transaction_id`。承兑订单。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `transaction_id` | bigint | 事务ID：18位，固定41+10位时间戳+4位序列+2位随机 |
| `request_no` | varchar(32) | 请求号 |
| `client_id` | varchar(32) | 客户端id |
| `accept_type` | varchar(10) | 承兑类型：T=交易, TR=交易退款 |
| `biz_product_code` | varchar(10) | 业务产品码 · 可空 |
| `currency` | varchar(10) | 法币币种 |
| `currency_amount` | decimal(19, 4) | 法币金额 |
| `gp_amount` | decimal(19, 4) | gp数量 |
| `exchange_rate` | int | 兑换汇率 |
| `extension` | varchar(255) | 扩展参数 · 可空 |
| `create_time` | timestamp | 创建时间 |

## 主键 / 索引
- 主键:`transaction_id`
- `idx_create_time`:create_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
