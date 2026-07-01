---
id: tbl_trade_t_trade_order
object_type: Table
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (trade schema) 2026-06-25
tags:
- trade
- trade
- t_trade_order
subdomain: trade
module: null
sensitivity: normal
name: 交易订单(t_trade_order)
aliases:
- t_trade_order
related_services:
- svc_tradeii
related_scenarios: []
---
# 交易订单(t_trade_order)

## 用途
交易订单。属 trade 库,由 [[svc_tradeii]] 读写。

## 关联关系
- **所属服务**:[[svc_tradeii]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `TRADE_VOUCHER_NO` | varchar(32) | PK / NOT NULL | 交易凭证号 |
| `TRADE_SRC_VOUCHER_NO` | varchar(64) | NOT NULL | 交易原始凭证号 |
| `ORIG_TRADE_VOUCHER_NO` | varchar(32) |  | 原交易凭证号 |
| `BIZ_NO` | varchar(64) |  | biz no |
| `BIZ_PRODUCT_CODE` | varchar(16) | NOT NULL | 产品编码 |
| `TRADE_AMOUNT` | decimal(15,4) | NOT NULL | 交易金额 |
| `pay_amount` | decimal(15,4) |  | 支付金额（不包含优惠金额）实际需要支付的法币 |
| `TRADE_TYPE` | varchar(16) | NOT NULL | 交易类型 |
| `GMT_SUBMIT` | timestamp | NOT NULL | 交易发起时间 |
| `BUYER_ID` | varchar(32) | NOT NULL | 买家客户ID |
| `BUYER_NAME` | varchar(128) |  | 买家客户名称 |
| `SELLER_ID` | varchar(32) | NOT NULL | 卖家客户ID |
| `SELLER_NAME` | varchar(128) |  | 卖家客户名称 |
| `SELLER_ACCOUNT_NO` | varchar(32) | NOT NULL | 卖家账户 |
| `PARTNER_ID` | varchar(32) | NOT NULL | 平台方客户ID |
| `PARTNER_NAME` | varchar(128) |  | 平台方客户名称 |
| `ACCESS_CHANNEL` | varchar(16) | NOT NULL | 终端类型 |
| `EXTENSION` | varchar(4000) |  | 扩展信息 |
| `PRE_STATUS` | varchar(16) |  | 前交易状态 |
| `STATUS` | varchar(16) | NOT NULL | 交易状态 |
| `TRADE_MEMO` | varchar(256) |  | 结果备注 |
| `RESULT_MEMO` | varchar(256) |  | result memo |
| `ERROR_CODE` | varchar(128) |  | 错误编码 |
| `ERROR_MSG` | varchar(256) |  | 错误信息 |
| `GMT_CREATE` | timestamp | NOT NULL / 默认 CURRENT_TIMESTAMP | 创建时间 |
| `GMT_MODIFIED` | timestamp |  | 修改时间 |
| `IS_NOTIFIED` | char |  | 当前状态的通知情况 Y-已通知 N-未通知 |
| `PROD_DESC` | varchar(1000) |  | 商品信息 |
| `PROD_SHOW_URL` | varchar(256) |  | 商品展示URL |
| `RELATED_TRADE_VOUCHER_NO` | varchar(32) |  | 关联交易凭证号（对应合并支付的交易） |
| `PROCESSOR_ID` | varchar(64) |  | 处理器ID |
| `PLATFORM_FEE` | decimal(15,4) |  | 平台方费用 |
| `PAYER_FEE` | decimal(15,4) |  | 付款方费用 |
| `PAYEE_FEE` | decimal(15,4) |  | 收款方费用 |
| `GMT_PAY_EXPIRED` | timestamp |  | pay expired time |
| `GMT_CLOSED` | timestamp |  | closed time |
| `GMT_FINISHED` | timestamp |  | finished time |
| `GMT_PAID` | timestamp |  | paid time |
| `SELLER_ACCOUNT_TYPE` | varchar(32) |  | 收款人账户类型 |
| `TRADE_BATCH_NO` | varchar(32) |  | trade batch no |
| `BUYER_IDENTITY_ID` | varchar(64) |  | 买方标志ID |
| `BUYER_IDENTITY_TYPE` | varchar(32) |  | 买方标志类型 |
| `SELLER_IDENTITY_ID` | varchar(64) |  | 卖方标志ID |
| `SELLER_IDENTITY_TYPE` | varchar(32) |  | 卖方标志类型 |
| `sub_status` | varchar(10) | NOT NULL / 默认 'init' | 结算与撤销子状态 初始init 撤销 cancel 结算 settle |
| `CURRENCY` | char(3) |  | 币种 |
| `gmt_estimated_time` | timestamp |  | 退款预估到账时间 同扩展参数 estimatedTime |

## 主键 / 索引
- 主键:(`TRADE_VOUCHER_NO`)
- 索引:
  - `IDX_SRC_V_NO` (TRADE_SRC_VOUCHER_NO)
  - `IDX_TO_GMT_PAY_EXPIRED` (GMT_PAY_EXPIRED)
  - `IDX_TO_ORIG_TRADE_VN` (ORIG_TRADE_VOUCHER_NO)
  - `IDX_TO_RELA_TRADE_VN` (RELATED_TRADE_VOUCHER_NO)
  - `IDX_TRADE_BATCH_NO` (TRADE_BATCH_NO)
  - `IDX_TRADE_GMT_MODIFIED` (GMT_MODIFIED)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
