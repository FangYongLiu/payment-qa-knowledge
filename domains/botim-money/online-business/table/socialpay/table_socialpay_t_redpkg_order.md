---
id: tbl_socialpay_t_redpkg_order
object_type: Table
name: 红包订单 (t_redpkg_order)
aliases: [t_redpkg_order, socialpay.t_redpkg_order]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: socialpay schema DDL
tags: [online-business, socialpay]
sensitivity: normal
related_services: []
---

# 红包订单 (t_redpkg_order)

## 用途
物理表 `socialpay.t_redpkg_order`,主键 `REDPKG_VOUCHER_NO`。红包订单。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `REDPKG_VOUCHER_NO` | varchar(32) | 主键 |
| `OUT_TRADE_NO` | varchar(64) | 外部商户订单号 |
| `PARTNER_ID` | varchar(32) | 待补 · 可空 |
| `SUBJECT` | varchar(60) | 待补 · 可空 |
| `BODY` | varchar(200) | 待补 · 可空 |
| `PAYER_UID` | varchar(64) | 付款人UID |
| `PAYER_MEMBER_ID` | varchar(32) | 付款方MEMBER_ID(42PAY) |
| `AMOUNT` | decimal(15, 4) | 待补 |
| `CURRENCY_CODE` | varchar(10) | 币种 |
| `REDPKG_TYPE` | varchar(20) | 红包类型 |
| `QUANTITY` | int(4) | 红包个数 |
| `REDPKG_STATUS` | varchar(15) | 红包状态 |
| `GMT_CREATED` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 修改时间 |
| `AVAILABLE_AMOUNT` | decimal(15, 4) | 可用金额 |
| `USING_AMOUNT` | decimal(15, 4) | 使用中的金额 |
| `RECEIVE_AMOUNT` | decimal(15, 4) | 已领取金额 |
| `RECEIVE_QUANTITY` | int(4) | 已领取次数 |
| `REFUNDED_AMOUNT` | decimal(15, 4) | 退款金额 |
| `EXTENSION` | varchar(500) | 扩展参数，JSON字符串 · 可空 |

## 主键 / 索引
- 主键:`REDPKG_VOUCHER_NO`
- `OUT_TRADE_NO`:OUT_TRADE_NO (UNIQUE)
- `T_REDPKG_ORDER`:OUT_TRADE_NO (UNIQUE)
- `t_redpkg_order_payer_member_id_index`:PAYER_MEMBER_ID
- `t_redpkg_order_payer_uid_index`:PAYER_UID

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
