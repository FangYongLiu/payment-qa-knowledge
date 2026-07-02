---
id: tbl_ccsales_t_sales_order
object_type: Table
name: 销售订单 (t_sales_order)
aliases: [t_sales_order, ccsales.t_sales_order]
domain: crypto
status: active
owner: can.wang
reviewer: can.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ccsales schema DDL
tags: [crypto, ccsales]
sensitivity: normal
related_services: []
---

# 销售订单 (t_sales_order)

## 用途
物理表 `ccsales.t_sales_order`,主键 `id`。销售订单。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id |
| `base_amount_crcy` | varchar(32) | 本位币币种 |
| `base_amount` | decimal(23, 8) | 本位币金额 |
| `quote_amount` | decimal(23, 8) | 报价金额 |
| `quote_amount_crcy` | varchar(32) | 报价币种 |
| `quote_id` | varchar(64) | 报价ID |
| `product_code` | varchar(16) | 产品码 |
| `symbol` | varchar(32) | symbol |
| `direction` | varchar(16) | 买卖方向 |
| `customer_mid` | varchar(32) | customerMid |
| `partner_id` | varchar(32) | partnerId |
| `exchange_mid` | varchar(32) | exchangeMerchantMid · 可空 |
| `status` | varchar(32) | status |
| `available_period` | timestamp(3) | 有效期 |
| `price` | decimal(23, 8) | 报价 |
| `fail_message` | varchar(128) | 错误原因 · 可空 |
| `fail_code` | varchar(32) | 错误码 · 可空 |
| `unity_result_code` | varchar(64) | 统一结果码 · 可空 |
| `created_time` | timestamp(3) | 创建时间 |
| `last_updated_time` | timestamp(3) | 最后更新时间 |
| `data_version` | bigint | 数据版本 |

## 主键 / 索引
- 主键:`id`
- `uk_sales_qi`:quote_id (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
