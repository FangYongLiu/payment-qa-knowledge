---
id: tbl_transfer_t_merchant_order
object_type: Table
name: 商户订单 (t_merchant_order)
aliases: [t_merchant_order, transfer.t_merchant_order]
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

# 商户订单 (t_merchant_order)

## 用途
物理表 `transfer.t_merchant_order`,主键 `merchant_order_no`。商户订单。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `merchant_order_no` | bigint | 订单号 |
| `request_order_no` | varchar(64) | 合作伙伴请求订单号 |
| `merchant_id` | varchar(20) | 商家ID |
| `payee_mid` | varchar(32) | 收款人ID |
| `payee_member_type` | char | 收款人类型: 1-个人,2-企业 |
| `payee_partner_id` | varchar(20) | 收款人平台 |
| `receive_amount` | decimal(19, 4) | 收款金额 |
| `currency` | char(3) | 币种 |
| `memo` | varchar(100) | Memo · 可空 |
| `notify_url` | varchar(150) | 通知地址 · 可空 |
| `push_bill_flag` | char(2) | 推送账单标志: Y - 已推送 · 可空 |
| `gmt_created` | timestamp | Create time |
| `gmt_modified` | timestamp | Update time |

## 主键 / 索引
- 主键:`merchant_order_no`
- `uk_o_m_uk`:request_order_no, merchant_id (UNIQUE)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
