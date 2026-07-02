---
id: tbl_pfhost_t_payment_record
object_type: Table
name: 支付记录表 (t_payment_record)
aliases: [t_payment_record, pfhost.t_payment_record]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: pfhost schema DDL
tags: [payment-core, pfhost]
sensitivity: normal
related_services: []
---

# 支付记录表 (t_payment_record)

## 用途
物理表 `pfhost.t_payment_record`,主键 `payment_voucher_no`。支付记录表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `payment_voucher_no` | bigint | 支付订单号 |
| `trade_voucher_no` | bigint | 交易订单号 |
| `member_id` | varchar(32) | 会员ID |
| `partner_id` | varchar(32) | 商户ID |
| `payment_no` | varchar(64) | 平台端支付订单号 |
| `order_token` | varchar(64) | 订单Token |
| `order_amount` | decimal(15, 4) | 订单金额 |
| `currency` | varchar(3) | 币种 |
| `notify_url` | varchar(128) | 通知地址 · 可空 |
| `addp_type` | varchar(64) | 额外验证项 · 可空 |
| `card_token` | varchar(64) | 卡Token · 可空 |
| `verify_result` | varchar(64) | 验证结果 · 可空 |
| `created_time` | timestamp | 创建时间 |
| `updated_time` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`payment_voucher_no`
- `idx_created_time`:created_time
- `idx_member_id`:member_id
- `idx_payment_no`:payment_no
- `idx_trade_voucher_no`:trade_voucher_no

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
