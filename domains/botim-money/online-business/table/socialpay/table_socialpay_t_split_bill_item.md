---
id: tbl_socialpay_t_split_bill_item
object_type: Table
name: AA收款账单项表 (t_split_bill_item)
aliases: [t_split_bill_item, socialpay.t_split_bill_item]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: socialpay schema DDL
tags: [online-business, socialpay]
sensitivity: normal
related_services: [svc_socialpay]
---

# AA收款账单项表 (t_split_bill_item)

## 用途
物理表 `socialpay.t_split_bill_item`,主键 `ID`。AA收款账单项表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `ID` | bigint(17) | 主键 |
| `BILL_ID` | bigint(17) | 账单ID |
| `BILL_ITEM_NO` | varchar(32) | AA分账 外部订单号 商户订单号 |
| `TRADE_VOUCHER_NO` | varchar(32) | 交易订单号 · 可空 |
| `PAYER_UID` | varchar(50) | 付款人Totok UID |
| `AMOUNT` | decimal(15, 4) | 支付金额 |
| `CURRENCY_CODE` | varchar(8) | 币种 |
| `STATUS` | varchar(16) | 支付状态 UNPAID:未付、PAID:已付、FAILED:失败 |
| `GMT_PAY` | timestamp | 支付完成时间 · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`ID`
- `BILL_ITEM_NO`:BILL_ITEM_NO (UNIQUE)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
