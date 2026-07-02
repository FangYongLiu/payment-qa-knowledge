---
id: tbl_instalment_t_ci_channel_order
object_type: Table
name: t_ci_channel_order (t_ci_channel_order)
aliases: [t_ci_channel_order, instalment.t_ci_channel_order]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: instalment schema DDL
tags: [lending, instalment]
sensitivity: normal
related_services: []
---

# t_ci_channel_order (t_ci_channel_order)

## 用途
物理表 `instalment.t_ci_channel_order`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int(11) | 主健 · 可空 |
| `channel_no` | varchar(64) | 渠道订单号 · 可空 |
| `out_order_no` | varchar(64) | 外部订单号 |
| `status` | smallint(5) | 0 进行中 1 成功 -1 失败 -2 退款 |
| `product_desc` | varchar(255) | 商品描述 · 可空 |
| `amount` | decimal(19, 2) | 金额 · 可空 |
| `refund_time` | timestamp | 退款时间 · 可空 |
| `refund_order_no` | varchar(64) | 退款订单号 · 可空 |
| `created_time` | timestamp | 创建时间 · 可空 |
| `last_modified` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_channel_no`:channel_no
- `idx_out_order_no`:out_order_no

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
