---
id: tbl_cspayment_tb_account_glide_01
object_type: Table
name: 入账流水 (tb_account_glide_01)
aliases: [tb_account_glide_01, cspayment.tb_account_glide_01]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: cspayment schema DDL
tags: [online-business, cspayment]
sensitivity: normal
related_services: []
---

# 入账流水 (tb_account_glide_01)

## 用途
物理表 `cspayment.tb_account_glide_01`,主键 `REQUEST_NO`。入账流水。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `REQUEST_NO` | varchar(32) | 请求号 |
| `CLEARING_SESSION_ID` | varchar(32) | 清算场次标识:SEQ_CLEARING_SESSION_ID |
| `PAYMENT_TYPE` | char(2) | I-入款,O-出款,T-转账,R-退款,F-退票 |
| `PAYMENT_SEQ_NO` | varchar(32) | 支付流水号 |
| `PRODUCT_CODE` | varchar(16) | 产品编码 |
| `PRODUCT_ORDER_NO` | varchar(32) | 产品订单号 |
| `FUNDS_CHANNEL` | varchar(16) | 资金渠道 |
| `INST_ORDER_NO` | varchar(32) | 机构订单号 |
| `AMOUNT` | decimal(15, 4) | 金额 |
| `CURRENCY` | char(3) | 币种 · 可空 |
| `PENDING_TYPE` | char | 入账类型：P-挂账；W-销帐 |
| `STATUS` | char | 流水状态：W-待发送；S-成功 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 最后修改时间 |

## 主键 / 索引
- 主键:`REQUEST_NO`
- `IDX_AG_CLEARING_SESSION_ID_01`:CLEARING_SESSION_ID
- `IDX_AG_GMTMODIFIED_01`:GMT_MODIFIED
- `IDX_AG_PAYMENT_SEQ_NO_01`:PAYMENT_SEQ_NO
- `idx_account_glide1_session_id`:CLEARING_SESSION_ID

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
