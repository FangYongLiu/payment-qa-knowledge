---
id: tbl_payment_tb_payment_order_08
object_type: Table
name: 支付指令 (tb_payment_order_08)
aliases: [tb_payment_order_08, payment.tb_payment_order_08]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: payment schema DDL
tags: [payment-core, payment]
sensitivity: normal
related_services: []
---

# 支付指令 (tb_payment_order_08)

## 用途
物理表 `payment.tb_payment_order_08`,主键 `PAYMENT_SEQ_NO`。支付指令。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `PAYMENT_SEQ_NO` | varchar(32) | YYYYMMDD||CODE[2]||SEQ_PAYMENT_ORDER[8] |
| `BIZ_PAYMENT_SEQ_NO` | varchar(32) | 业务支付订单流水号 |
| `RELATE_PAYMENT_SEQ_NO` | varchar(32) | 相关支付流水号 · 可空 |
| `PAYMENT_TYPE` | varchar(10) | 待补 |
| `PRODUCT_CODE` | varchar(32) | 产品编码 |
| `PAYMENT_CODE` | varchar(16) | 支付编码 |
| `PRODUCT_ORDER_NO` | varchar(64) | 产品订单号，产品体系内生成 |
| `PAYMENT_ORDER_NO` | varchar(64) | 支付订单号，收单服务支付订单流水号 |
| `GMT_PAYMENT` | timestamp | 支付发起时间 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 最后修改时间 |
| `MEMO` | varchar(256) | 备注 · 可空 |
| `PAY_MODE` | varchar(32) | 支付模式 · 可空 |
| `PAY_CHANNEL` | varchar(16) | 支付渠道 · 可空 |
| `PS_CODE` | varchar(16) | 支付服务码 · 可空 |
| `AUTO_SETTLE` | char | 是否自动结算 · 可空 |

## 主键 / 索引
- 主键:`PAYMENT_SEQ_NO`
- `IDX_PAYMENT_ORDER_BPSN_08`:BIZ_PAYMENT_SEQ_NO
- `IDX_PAYMENT_ORDER_CREATE_08`:GMT_CREATE
- `IDX_PAYMENT_ORDER_MODIFIED_08`:GMT_MODIFIED
- `IDX_PAYMENT_ORDER_PO_08`:PAYMENT_ORDER_NO
- `IDX_PAYMENT_ORDER_RPSN_08`:RELATE_PAYMENT_SEQ_NO

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
