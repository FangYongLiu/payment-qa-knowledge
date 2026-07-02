---
id: tbl_marketorder_t_life_bill
object_type: Table
name: 生活应用账单表 (t_life_bill)
aliases: [t_life_bill, marketorder.t_life_bill]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: marketorder schema DDL
tags: [marketing, marketorder]
sensitivity: normal
related_services: []
---

# 生活应用账单表 (t_life_bill)

## 用途
物理表 `marketorder.t_life_bill`,主键 `id`。生活应用账单表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(18) | 主键 · 可空 |
| `ticket_no` | varchar(32) | 票据号 · 可空 |
| `account_no` | varchar(32) | 账户号 · 可空 |
| `service_provider` | varchar(16) | 服务商 · 可空 |
| `supplier_no` | varchar(32) | 账单所属供应商编号 · 可空 |
| `channel_code` | varchar(32) | 账单所属渠道 · 可空 |
| `bill_amount` | decimal(15, 4) | 账单金额 · 可空 |
| `currency` | varchar(10) | 币种 |
| `pay_output_item` | varchar(150) | 支付凭据 · 可空 |
| `gmt_created` | timestamp | 创建时间 |
| `bill_type` | varchar(50) | 账单类型：话费后付费账单-MOBILE_POSTPAID 停车缴费账单-PARKING_BILL,水电费账单-WATER_ELECTRIC · 可空 |
| `min_amt` | decimal(15, 4) | 最小账单金额 · 可空 |
| `max_amt` | decimal(15, 4) | 最大账单金额 · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
