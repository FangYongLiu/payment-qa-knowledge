---
id: tbl_deposit_t_payment_order
object_type: Table
name: 充值支付订单 (t_payment_order)
aliases: [t_payment_order, deposit.t_payment_order]
domain: deposit-vam
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: deposit schema DDL
tags: [deposit-vam, deposit]
sensitivity: normal
related_services: []
---

# 充值支付订单 (t_payment_order)

## 用途
物理表 `deposit.t_payment_order`,主键 `PAYMENT_VOUCHER_NO`。充值支付订单。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `PAYMENT_VOUCHER_NO` | varchar(32) | 支付凭证号，主键，统一凭证 |
| `TRADE_VOUCHER_NO` | varchar(32) | 订单凭证号 · 可空 |
| `PRODUCT_CODE` | varchar(16) | 支付产品编码 |
| `MEMBER_ID` | varchar(32) | 客户ID |
| `ACCOUNT_NO` | varchar(32) | 用户账户 · 可空 |
| `AMOUNT` | decimal(15, 2) | 金额 |
| `FEE` | decimal(15, 2) | 费用 · 可空 |
| `PAY_MODE` | varchar(32) | 支付模式 · 可空 |
| `PAY_CHANNEL` | varchar(32) | 支付渠道 · 可空 |
| `pay_scene` | varchar(32) | 支付场景 · 可空 |
| `REMARK` | varchar(128) | 支付说明 · 可空 |
| `GMT_PAY_SUBMIT` | timestamp | 支付提交时间 · 可空 |
| `PAYMENT_STATUS` | varchar(16) | 支付状态 · 可空 |
| `EXT` | varchar(4000) | 扩展参数 · 可空 |
| `BIZ_PAYMENT_SEQ_NO` | varchar(32) | 业务支付流水号 · 可空 |
| `BIZ_PAYMENT_STATE` | varchar(16) | 业务支付状态 · 可空 |
| `BIZ_SUB_STATE` | varchar(16) | 业务支付子状态 · 可空 |
| `INST_PAY_NO` | varchar(64) | 机构支付编码 · 可空 |
| `GMT_PAID` | timestamp | 支付完成时间 · 可空 |
| `ACCESS_CHANNEL` | varchar(16) | 终端类型 · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 修改时间 · 可空 |
| `MERCHANT_NOTIFY_STATUS` | varchar(16) | 商户通知状态 · 可空 |
| `USER_NOTIFY_STATUS` | varchar(16) | 用户通知状态 · 可空 |
| `PARTNER_FEE` | decimal(15, 2) | 平台方费用 · 可空 |
| `ACCOUNT_TYPE` | varchar(16) | 账户类型 · 可空 |
| `CHARGE_FEE` | decimal(15, 2) | SINA收取用户费用 · 可空 |
| `currency` | char(3) | 货币 中国CNY 阿联酋 AED 对应java类 Currency · 可空 |

## 主键 / 索引
- 主键:`PAYMENT_VOUCHER_NO`
- `IDX_PAYMENT_ORDER_T_V_NO`:TRADE_VOUCHER_NO
- `I_PAYMENT_ORDER_SUBMIT`:GMT_PAY_SUBMIT

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
