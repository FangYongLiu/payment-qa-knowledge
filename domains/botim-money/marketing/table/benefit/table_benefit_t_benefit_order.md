---
id: tbl_benefit_t_benefit_order
object_type: Table
name: t_benefit_order (t_benefit_order)
aliases: [t_benefit_order, benefit.t_benefit_order]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: benefit schema DDL
tags: [marketing, benefit]
sensitivity: normal
related_services: []
---

# t_benefit_order (t_benefit_order)

## 用途
物理表 `benefit.t_benefit_order`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 自增id · 可空 |
| `partner_id` | varchar(32) | 合作方id |
| `member_id` | varchar(32) | 会员id |
| `earnings_detail_id` | bigint | 收益明细id |
| `earnings_amount` | decimal(19, 4) | 收益金额 · 可空 |
| `currency` | varchar(3) | 收益金额币种 · 可空 |
| `biz_product_code` | varchar(20) | 产品码 · 可空 |
| `order_no` | varchar(64) | 订单号 · 可空 |
| `status` | varchar(10) | P S F · 可空 |
| `payer_member_id` | varchar(50) | 付款方会员id · 可空 |
| `payer_account_type` | varchar(255) | 付款方账户类型 · 可空 |
| `result_code` | varchar(128) | 返回码 · 可空 |
| `result_msg` | varchar(255) | 返回信息 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 更新时间 |
| `merchant_id` | varchar(32) | 商户id |

## 主键 / 索引
- 主键:`id`
- `idx_order_no`:order_no (UNIQUE)
- `idx_create_time`:create_time
- `idx_earnings_detail_id`:earnings_detail_id, status

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
