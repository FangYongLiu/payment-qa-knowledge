---
id: tbl_tts_t_relate_order
object_type: Table
name: Relate order (t_relate_order)
aliases: [t_relate_order, tts.t_relate_order]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: tts schema DDL
tags: [lending, tts]
sensitivity: normal
related_services: []
---

# Relate order (t_relate_order)

## 用途
物理表 `tts.t_relate_order`,主键 `relate_voucher_no`。Relate order。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `relate_voucher_no` | bigint(21) | relate voucher no |
| `order_type` | varchar(2) | Order Type: RO-Refund |
| `pay_voucher_no` | bigint(21) | pay voucher no |
| `amount` | decimal(20, 4) | amount |
| `currency` | char(3) | currency |
| `order_status` | char | Order Status: P-Processing, F-Fail, S-Success |
| `memo` | varchar(128) | memo · 可空 |
| `extension` | varchar(255) | extension · 可空 |
| `gmt_create` | timestamp(3) | create time |
| `gmt_modified` | timestamp(3) | modify time · 可空 |

## 主键 / 索引
- 主键:`relate_voucher_no`
- `idx_relate_order_pay_no`:pay_voucher_no

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
