---
title: 收单商户控台(Acquire Merchant Console)
domain: merchant-portal
kind: wiki_page
slug: acquire-merchant-console
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:fa5361b9-9768-4302-b8dc-f2dd9cc50451
tags: []
---

# 收单商户控台(Acquire Merchant Console)

收单商户控台面向已选择 `Payment` 业务类型(Merchant Acquire Service)的商户，提供支付产品申请、交易/账户/对账单查询、线下 POS 设备管理与商户设置等能力，并依赖 BMOC 后台进行审核与开通。

## 前置条件与入口

- 需先完成 Botim 商户注册并通过 Onboarding，详见 [[merchant-onboarding-flow]]。
- 通过商户控台登录后，选择 `Payment` 进入收单控台。
- 控台总览参见 [[merchant-portal-overview]]。

## 功能概览

- 申请支付产品(Apply for payment products)
- 设置商户 API
- 查询收单交易(Query acquiring transactions)
- 查询账户余额(Query account balance)
- 商户对账单(Merchant statement)
- 资金 Top up、Withdraw、Transfer
- 申请线下 POS 设备

## 支付产品申请(Apply for payment products)

支持两种申请方式，最终都需要在 BMOC 进行审核。

- **Method 1**：商户在控台菜单主动申请产品 → 进入 BMOC 审核。
- **Method 2**：业务团队在 BMOC 系统直接为商户开通产品。
  - 申请路径：`Basis-merchant => General => ProductOpenMgt => Merchant Open Product`
  - 审核路径：`Basis-merchant => General => Product Audit => Apply Audit`

### 产品与 System Product Code

| Product Name | API Payment Scenarios | System Product Code |
|---|---|---|
| Basic Payment Gateway | DYNQR / JSAPI / PAYPAGE / EWALLET | 200101 |
| INAPP | INAPP | 200102 |
| Face Pay | Face Pay | 200103 |
| Direct Pay | Direct Pay | 200104 |
| ADCB POS | ADCB POS | 200105 |
| Smart Purchase | DYNQR, QRPAY | 200201 |
| QRPAY | QRPAY | 200301 |
| Auto Debit | Authorized payment | 200401 |
| Smart Code | SCQR | 210401 |
| Cash Top Up | Offline cash top-up | 200601 |

### 数据库校验(ppcenter)

| Table | Field Check |
|---|---|
| `t_product_apply_order` | status : `S` |
| `t_product_apply_info` | — |
| `t_merchant_product_order` | — |

测试场景详见 [[scn_acquire_product_apply]]。

## 交易查询(Transactions)

记录商户的各类交易，包括：order processing、refunds、withdrawals、transfers to individuals、transfers to banks、VAM top-ups。

数据库校验：

| Database | Table | Field Check |
|---|---|---|
| acquireii | `t_acquire_order` | status : `S` |
| acquireii | `t_refund_order` | — |
| mhtfundout | `t_withdraw_order` | — |
| mhtfundout | `t_fundout_order` | — |
| mhtfundout | `t_fundout_bankcard_order` | — |
| deposit | `t_deposit_order` | — |

## 账户(Account)

展示商户当前可提现余额与在途交易。

数据库校验：

| Database | Table |
|---|---|
| dpm | `t_dpm_outer_account_sub_detail` |
| dpm | `t_dpm_outer_account_subset` |

## 对账单(Statements)

包含交易对账单(transaction statements)与结算对账单(settlement statements)；由每日凌晨定时 JOB 批量生成。

数据库校验(statementii)：

- `t_statement_transaction`
- `t_statement_settlement`
- `t_statement_balance`
- `t_statement_subscribe`

## 线下业务(Offline Business)

线下 POS 设备的申请与激活流程：

1. 控台页面进行设备申请与激活管理。
2. BMOC 审核：`Basis--merchant => Device Approval`。

数据库校验：

| Database | Table |
|---|---|
| merchant | `t_store` |
| device | `t_device_apply_order` |
| device | `t_active_code` |
| device | `t_merchant_device` |
| device | `t_device_key` |
| device | `t_destroyed_device` |

## 商户设置(Merchant Settings)

涵盖商户基础信息、绑卡、员工与角色、结算配置等。其中 `t_settlement_config` 用于配置 Reserved Amount、Minimum Withdrawal Amount 等结算参数。

数据库校验：

| Database | Table |
|---|---|
| merchant | `t_merchant` |
| merchant | `t_binding_card_apply_info` |
| merchant | `t_staff` |
| merchant | `t_staff_role` |
| statementii | `t_settlement_config` |

## 相关参考

- DB/Redis/Kibana 访问方式：[[qa-infra-access-guide]]
- 服务应用 Owner 清单：[[merchant-portal-service-components]]
- Onboarding 数据库影响范围：[[merchant-onboarding-database-scope]]
