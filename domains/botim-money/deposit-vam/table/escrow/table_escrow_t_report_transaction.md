---
id: tbl_escrow_t_report_transaction
object_type: Table
name: 报告订单列表 (t_report_transaction)
aliases: [t_report_transaction, escrow.t_report_transaction]
domain: deposit-vam
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: escrow schema DDL
tags: [deposit-vam, escrow]
sensitivity: normal
related_services: []
---

# 报告订单列表 (t_report_transaction)

## 用途
物理表 `escrow.t_report_transaction`,主键 `transaction_id`。报告订单列表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `transaction_id` | bigint | 订单id · 可空 |
| `fund_id` | varchar(32) | 资金id |
| `voucher_no` | varchar(32) | 支付请求号 · 可空 |
| `payment_order_no` | varchar(32) | 支付订单号 · 可空 |
| `auth_code` | varchar(6) |  授权码 · 可空 |
| `member_id` | varchar(16) | 会员id · 可空 |
| `card_id` | varchar(18) | 卡id |
| `amount` | decimal(16, 2) | 金额 |
| `currency` | char(3) | 币种 · 可空 |
| `direction` | varchar(10) | 方向,positive-加,negetive-减 |
| `report_record_id` | varchar(32) | 报告记录id，批次 · 可空 |
| `report_status` | varchar(1) | 上报状态,I-初始,P-上报中,S-成功,F-上报失败 · 可空 |
| `report_category` | varchar(32) | 上报类型 · 可空 |
| `transaction_type` | varchar(6) | 交易类型 · 可空 |
| `after_balance` | decimal(16, 2) | 后余额 · 可空 |
| `biz_product_code` | varchar(6) | 业务产品码 · 可空 |
| `clearing_code` | varchar(32) | 清算编码 · 可空 |
| `merge_id` | bigint | Merge Id |
| `gmt_fund` | timestamp(6) | 入账时间 · 可空 |
| `gmt_create` | timestamp(6) | 创建时间 |
| `gmt_modified` | timestamp(6) | 修改时间 · 可空 |
| `memo` | varchar(64) | 备注 · 可空 |
| `return_status` | varchar(32) | 返回状态 · 可空 |
| `bank_balance` | varchar(32) | 银行余额 · 可空 |
| `extension` | varchar(128) | 拓展信息 · 可空 |

## 主键 / 索引
- 主键:`transaction_id`
- `uk_report_tranaction_fund_id`:fund_id (UNIQUE)
- `idx_memberid`:member_id
- `idx_report_txn_clearing`:report_record_id, report_category
- `idx_trans_merge_id`:merge_id
- `indx_gmt_create_stat`:gmt_create, report_status
- `indx_gmt_fund`:gmt_fund

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
