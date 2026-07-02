---
id: tbl_fundout_tt_payment_order
object_type: Table
domain: fundout
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (fundout schema) 2026-06-25
tags:
- fundout
- fundout
- tt_payment_order
subdomain: fundout
module: null
sensitivity: normal
name: 出款支付订单(tt_payment_order)
aliases:
- tt_payment_order
related_services:
- svc_fundout
related_scenarios: []
---
# 出款支付订单(tt_payment_order)

## 用途
出款支付订单。属 fundout 库,由 [[svc_fundout]] 读写。

## 关联关系
- **所属服务**:[[svc_fundout]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `PAYMENT_ORDER_NO` | varchar(32) | PK / NOT NULL | 出款支付凭证号 |
| `FUNDOUT_ORDER_NO` | varchar(32) |  | 出款交易凭证号 |
| `MEMBER_ID` | varchar(32) |  | 会员编号(该会员作为付款方参与交易) |
| `PRODUCT_CODE` | varchar(32) |  | 产品编码 |
| `ACCOUNT_NO` | varchar(32) |  | 储值账户 |
| `BANK_CODE` | varchar(32) |  | 银行编码 |
| `CARD_NO` | varchar(32) |  | 银行卡卡号 |
| `AMOUNT` | decimal(18,2) |  | 支付金额 |
| `FEE` | decimal(18,2) |  | 手续费 |
| `STATUS` | varchar(16) |  | 申请成功，提交银行成功，成功，失败，退票 |
| `NOTIFY_STATUS` | char |  | 通知状态 |
| `ORDER_TIME` | timestamp |  | 下单时间 |
| `RESULT_TIME` | timestamp |  | 订单状态对应时间 |
| `EXTENSION` | varchar(2000) |  | 记录出款明细 |
| `GMT_CREATE` | timestamp |  | 创建时间 |
| `GMT_MODIFY` | timestamp |  | 更新时间 |
| `NAME` | varchar(256) |  | 银行卡户名 |
| `COMPANY_PERSONAL` | char |  | 对公/对私 |
| `PARTNER_FEE` | decimal(15,2) |  | 平台方费用 |
| `ACCOUNT_TYPE` | varchar(16) |  | 账户类型 |
| `CHARGE_FEE` | decimal(15,2) |  | SINA收取用户费用 |
| `return_fee` | decimal(19,4) |  | 退款退费金额 |
| `currency` | char(3) |  | 货币 中国CNY 阿联酋 AED 对应java类 Currency |

## 主键 / 索引
- 主键:(`PAYMENT_ORDER_NO`)
- 唯一约束:
  - `UK_FUNDOUT_ORDER_KEY` 唯一 (FUNDOUT_ORDER_NO)
- 索引:
  - `IDX_PAYMENT_GMT_MODIFY` (GMT_MODIFY)
  - `I_MEMBER_ID` (MEMBER_ID)
  - `I_ORDER_TIME` (ORDER_TIME)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
