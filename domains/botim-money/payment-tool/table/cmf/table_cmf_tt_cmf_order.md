---
id: tbl_cmf_tt_cmf_order
object_type: Table
name: 渠道支付订单 (tt_cmf_order)
aliases: [tt_cmf_order, cmf.tt_cmf_order]
domain: payment-tool
status: active
owner: kingo.liang
reviewer: kingo.liang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: cmf schema DDL
tags: [payment-tool, cmf]
sensitivity: normal
related_services: []
---

# 渠道支付订单 (tt_cmf_order)

## 用途
物理表 `cmf.tt_cmf_order`,主键 `CMF_SEQ_NO`。渠道支付订单。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `CMF_SEQ_NO` | varchar(32) | 渠道流水号，yyyymmdd+seq_cmf_order |
| `PAYMENT_SEQ_NO` | varchar(32) | 支付流水号 |
| `REQUEST_BATCH_NO` | varchar(32) | 请求批次号 · 可空 |
| `ORDER_TYPE` | char | 订单类型：I（入款），B（退款），O（出款） |
| `PRODUCT_CODE` | varchar(32) | 产品码 |
| `PAYMENT_CODE` | varchar(32) | 支付编码 |
| `MEMBER_ID` | varchar(64) | 会员ID,现阶段是PT帐号 · 可空 |
| `AMOUNT` | decimal(15, 2) | 金额 |
| `CURRENCY` | char(3) | 币种 |
| `INST_CODE` | varchar(32) | 机构编码 · 可空 |
| `PAYMENT_NOTIFY_STATUS` | char | 支付结果通知状态：S（通知成功），F（通知失败），N（不通知） · 可空 |
| `COMMUNICATE_TYPE` | char | 通信类型，S（单笔通信），B（批量通信） · 可空 |
| `STATUS` | char | 状态：A（待处理），C（已撤销），I（处理中），S（成功），F（失败） · 可空 |
| `OPERATOR` | varchar(32) | 操作员，默认SYSTEM · 可空 |
| `GMT_SUBMIT` | timestamp | 提交时间 · 可空 |
| `INST_ORDER_ID` | decimal(19) | 机构订单ID · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `BIZ_DATE` | char(16) | 业务发生时间 · 可空 |
| `GMT_MODIFIED` | timestamp | 最后修改时间 |
| `MEMO` | varchar(128) | 备注 · 可空 |
| `CONFIRM_STATUS` | char | 配置状态 |
| `PAY_MODE` | varchar(32) | 支付方式 · 可空 |
| `SUBMIT_BATCH_NO` | varchar(32) | 提交批次号 · 可空 |
| `ORGI_PAYMENT_SEQ_NO` | varchar(32) | 原始支付流水号 · 可空 |
| `EXPECT_TIME` | timestamp | 期望时间 · 可空 |
| `EXTENSION` | varchar(2048) | 扩展信息 · 可空 |
| `SETTLEMENT_ID` | varchar(32) | 结算id · 可空 |
| `ORGI_SETTLEMENT_ID` | varchar(32) | 原订单结算id · 可空 |
| `PAYMENT_VOUCHER_NO` | varchar(32) | 统一支付凭证 · 可空 |
| `MERCHANT_ID` | varchar(32) | 商户id · 可空 |

## 主键 / 索引
- 主键:`CMF_SEQ_NO`
- `IX_TTCMFORDER_GMTCREATE`:GMT_CREATE
- `IX_TTCMFORDER_INSTORDERID`:INST_ORDER_ID
- `IX_TTCMFORDER_PAYMENTSEQNO`:PAYMENT_SEQ_NO
- `IX_TTCMFORDER_SETTLEMENTID`:SETTLEMENT_ID
- `idx_VOUNOP_CTIME`:PAYMENT_VOUCHER_NO, GMT_CREATE
- `idx_ttcmforder_osi`:ORGI_SETTLEMENT_ID

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
