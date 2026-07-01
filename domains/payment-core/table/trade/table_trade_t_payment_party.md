---
id: tbl_trade_t_payment_party
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
- t_payment_party
subdomain: trade
module: null
sensitivity: normal
name: 支付参与方(t_payment_party)
aliases:
- t_payment_party
related_services:
- svc_tradeii
related_scenarios: []
---
# 支付参与方(t_payment_party)

## 用途
支付参与方。属 trade 库,由 [[svc_tradeii]] 读写。

## 关联关系
- **所属服务**:[[svc_tradeii]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `PAYMENT_PARTY_ID` | decimal(17) | PK / NOT NULL | 参与方ID |
| `PAYMENT_VOUCHER_NO` | varchar(32) |  | 支付凭证号 |
| `PARTY_ID` | varchar(32) | NOT NULL | 客户ID |
| `ROLE_CODE` | varchar(16) | NOT NULL | 角色 |
| `ACCOUNT_NO` | varchar(32) |  | 账户 |
| `AMOUNT` | decimal(15,4) | NOT NULL | 金额 |
| `FEE` | decimal(15,2) |  | 费用 |
| `GMT_CREATE` | timestamp | NOT NULL / 默认 CURRENT_TIMESTAMP | 创建时间 |
| `GMT_MODIFIED` | timestamp |  | 修改时间 |
| `ACCOUNT_TYPE` | varchar(32) |  | 账户类型 |
| `FROZEN_AMOUNT` | decimal(15,4) |  | 冻结金额 |
| `UNFROZEN_AMOUNT` | decimal(15,4) |  | 解冻金额 |
| `CURRENCY` | char(3) |  | 币种 |
| `extension` | varchar(100) |  | 扩展参数 |

## 主键 / 索引
- 主键:(`PAYMENT_PARTY_ID`)
- 索引:
  - `IDX_PP_PAYMENT_VN` (PAYMENT_VOUCHER_NO)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
