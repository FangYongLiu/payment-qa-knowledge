---
id: tbl_transfer_t_split_sub_bill
object_type: Table
name: 分账子订单表 (t_split_sub_bill)
aliases: [t_split_sub_bill, transfer.t_split_sub_bill]
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

# 分账子订单表 (t_split_sub_bill)

## 用途
物理表 `transfer.t_split_sub_bill`,主键 `sub_bill_no`。分账子订单表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `sub_bill_no` | bigint | 子账单账单编号 |
| `bill_no` | bigint | 账单编号 |
| `payment_no` | bigint | 付款订单号 · 可空 |
| `sub_bill_amount` | decimal(15, 4) | 子账单金额 |
| `currency` | varchar(10) | 币种 |
| `payer_mid` | varchar(32) | 付款人mid · 可空 |
| `payer_uid` | varchar(64) | 付款人uid · 可空 |
| `partner_id` | varchar(32) | 付款人平台 · 可空 |
| `payment_name` | varchar(50) | 付款人昵称 · 可空 |
| `payment_source` | varchar(15) | 付款源(BUMP:碰一碰、SMS:短信、QRCODE:二维码、SHARE_LINK:分享链接) · 可空 |
| `status` | varchar(20) | 状态(INIT:初始化、PAY_SUCCESS:付款成功,EXPIRED) |
| `memo` | varchar(100) | 备注 · 可空 |
| `gmt_created` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改时间 |
| `share_user_id` | varchar(32) | 分享用户id · 可空 |

## 主键 / 索引
- 主键:`sub_bill_no`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
