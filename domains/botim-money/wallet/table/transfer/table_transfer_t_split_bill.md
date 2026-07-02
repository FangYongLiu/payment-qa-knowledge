---
id: tbl_transfer_t_split_bill
object_type: Table
name: 分账总账单表 (t_split_bill)
aliases: [t_split_bill, transfer.t_split_bill]
domain: wallet
status: active
owner: qianlong.wang
reviewer: qianlong.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: transfer schema DDL
tags: [wallet, transfer]
sensitivity: normal
related_services: []
---

# 分账总账单表 (t_split_bill)

## 用途
物理表 `transfer.t_split_bill`,主键 `bill_no`。分账总账单表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `bill_no` | bigint | 账单编号 |
| `receive_mid` | varchar(32) | 收款人mid |
| `receive_uid` | varchar(64) | 收款人uid |
| `partner_id` | varchar(32) | 收款人平台 |
| `receive_name` | varchar(100) | 收款人名字 · 可空 |
| `bill_type` | varchar(20) | 账单类型(AVG:均分、CM:定制) |
| `bill_amount` | decimal(15, 4) | 账单金额 |
| `receivable_amount` | decimal(15, 4) | 应收金额 |
| `received_amount` | decimal(15, 4) | 已收金额 · 可空 |
| `currency` | varchar(10) | 币种 |
| `people_number` | int(4) | 分账人数 |
| `real_people_number` | int(4) | 实际分账人数 |
| `received_number` | int(4) | 已收子账单数 · 可空 |
| `status` | varchar(20) | 状态(RECEIVING:收款中、RECEIVE_SUCCESS、RECEIVE_FAILED、EXPIRED) |
| `memo` | varchar(100) | 备注 · 可空 |
| `expire_time` | timestamp | 过期时间 · 可空 |
| `gmt_created` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改时间 |
| `merchant_order_no` | bigint | 商家订单号 · 可空 |

## 主键 / 索引
- 主键:`bill_no`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
