---
id: tbl_payment_tb_funds_payment_ctrl
object_type: Table
name: 用来控制收单产品同一个产品订单号下只有一个机构支付成功 (tb_funds_payment_ctrl)
aliases: [tb_funds_payment_ctrl, payment.tb_funds_payment_ctrl]
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

# 用来控制收单产品同一个产品订单号下只有一个机构支付成功 (tb_funds_payment_ctrl)

## 用途
物理表 `payment.tb_funds_payment_ctrl`,主键 `CTRL_ID`。用来控制收单产品同一个产品订单号下只有一个机构支付成功。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `CTRL_ID` | decimal(18) | 主键 |
| `PRODUCT_CODE` | varchar(32) | 产品编码 |
| `PRODUCT_ORDER_NO` | varchar(64) | 产品订单号 |
| `PAYMENT_SEQ_NO` | varchar(32) | 成功支付流水号 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 最后修改时间 |

## 主键 / 索引
- 主键:`CTRL_ID`
- `UIDX_PN`:PRODUCT_CODE, PRODUCT_ORDER_NO (UNIQUE)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
