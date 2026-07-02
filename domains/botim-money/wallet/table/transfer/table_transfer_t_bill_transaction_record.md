---
id: tbl_transfer_t_bill_transaction_record
object_type: Table
name: 账单交易记录 (t_bill_transaction_record)
aliases: [t_bill_transaction_record, transfer.t_bill_transaction_record]
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

# 账单交易记录 (t_bill_transaction_record)

## 用途
物理表 `transfer.t_bill_transaction_record`,主键 `transaction_id`。账单交易记录。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `transaction_id` | bigint | 交易id |
| `bill_no` | bigint | 账单编号 |
| `sub_bill_no` | bigint | 子账单账单编号 |
| `payer_mid` | varchar(32) | 付款人mid |
| `payer_uid` | varchar(64) | 付款人uid |
| `partner_id` | varchar(32) | 付款人平台 |
| `payment_name` | varchar(150) | 付款人昵称 · 可空 |
| `payment_source` | varchar(15) | 付款源(BUMP:碰一碰、SMS:短信、QRCODE:二维码、SHARE_LINK:分享链接) |
| `payment_no` | bigint | 付款订单号 · 可空 |
| `status` | varchar(20) | 状态(PAYING:付款中、PAY_SUCCESS:付款成功、TRADE_FAILED:交易失败) |
| `version` | int(4) | 版本(对同一笔sub_bill_no) |
| `gmt_created` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`transaction_id`
- `uk_btr_subbillno_s_v`:sub_bill_no, version (UNIQUE)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
