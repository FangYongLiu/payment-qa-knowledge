---
id: tbl_trade_t_split_party
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
- t_split_party
subdomain: trade
module: null
sensitivity: normal
name: 分账信息扩展(t_split_party)
aliases:
- t_split_party
related_services:
- svc_tradeii
related_scenarios: []
---
# 分账信息扩展(t_split_party)

## 用途
分账信息扩展。属 trade 库,由 [[svc_tradeii]] 读写。

## 关联关系
- **所属服务**:[[svc_tradeii]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `SPLIT_ID` | decimal(17) | PK / NOT NULL | 分账信息ID |
| `TRADE_VOUCHER_NO` | varchar(32) |  | 交易凭证号 |
| `PAYER_ID` | varchar(32) |  | 付款方客户ID |
| `PAYER_ACCOUNT_NO` | varchar(32) |  | 付款方账户 |
| `PAYEE_ID` | varchar(32) | NOT NULL | 收款方客户ID |
| `PAYEE_ACCOUNT_NO` | varchar(32) | NOT NULL | 收款方账户 |
| `SPLIT_TAG` | varchar(16) |  | 分账类型 |
| `SPLIT_ORDER` | decimal(3) |  | 分账顺序 |
| `AMOUNT` | decimal(15,4) | NOT NULL | 金额 |
| `MEMO` | varchar(256) |  | 备注 |
| `GMT_CREATE` | timestamp | NOT NULL / 默认 CURRENT_TIMESTAMP | 创建时间 |
| `GMT_MODIFIED` | timestamp |  | 修改时间 |
| `PAYER_IDENTITY` | varchar(32) |  | 付款方标识 |
| `PAYER_IDENTITY_TYPE` | varchar(16) |  | 付款方标识类型 |
| `PAYER_ACCOUNT_TYPE` | varchar(16) |  | 付款方账户类型 |
| `PAYEE_IDENTITY` | varchar(32) |  | 收款方标识 |
| `PAYEE_IDENTITY_TYPE` | varchar(16) |  | 收款方标识类型 |
| `PAYEE_ACCOUNT_TYPE` | varchar(16) |  | 收款方账户类型 |
| `CURRENCY` | char(3) |  | 币种 |

## 主键 / 索引
- 主键:(`SPLIT_ID`)
- 索引:
  - `IDX_SPLIT_PARTY_PAYEE_ID` (PAYEE_ID)
  - `IDX_SPLIT_PARTY_PAYER_ID` (PAYER_ID)
  - `IDX_TSP_TRADE_VN` (TRADE_VOUCHER_NO)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
