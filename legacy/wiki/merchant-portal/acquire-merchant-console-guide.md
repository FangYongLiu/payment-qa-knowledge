---
title: 收单商户控台(Acquire Merchant Console)使用指南
domain: merchant-portal
kind: wiki_page
slug: acquire-merchant-console-guide
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/997785804
tags: []
---

# 收单商户控台(Acquire Merchant Console)使用指南

本页介绍商户在完成 Botim 注册并选择 Payment 业务类型后，进入收单商户控台进行支付产品申请、交易/账户/对账单查询、线下设备管理及商户设置的功能要点与对应数据库校验。

## 前置条件与功能概览

进入控台前需先完成商户注册与入驻流程，详见 [[merchant-onboarding-flow]]；环境地址、登录账号与基础设施访问参考 [[merchant-portal-env-access-guide]]。

- 前置：先注册为 Botim Merchant，并通过商户门户登录，业务类型选择 `Payment`
- 主要功能：
  - 申请支付产品
  - 设置 Merchant API
  - 查询收单交易
  - 查询账户余额
  - 商户对账单
  - 充值、提现、转账
  - 申请线下 POS 设备

## 申请支付产品 (Apply for payment products)

支持两种申请路径：

- Method 1：商户在控台菜单中主动申请产品，再到 BMOC 系统审核
- Method 2：业务团队直接在 BMOC 系统中为商户开通产品
  - Apply 菜单：`Basis-merchant => General => ProductOpenMgt => Merchant Open Product`
  - Audit 菜单：`Basis-merchant => General => Product Audit => Apply Audit`

端到端流程详见 [[flow_acquire_product_application]]。

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

### Database Check

库 `ppcenter`：

- `t_product_apply_order` — `status: S`
- `t_product_apply_info`
- `t_merchant_product_order`

## 交易 (Transactions)

记录商户各类交易：订单处理、退款、提现、个人转账、银行转账、VAM 充值。

### Database Check

| Database | Table | Field Check |
|---|---|---|
| acquireii | t_acquire_order | status : S |
| acquireii | t_refund_order | |
| mhtfundout | t_withdraw_order | |
| mhtfundout | t_fundout_order | |
| mhtfundout | t_fundout_bankcard_order | |
| deposit | t_deposit_order | |

## 账户 (Account)

记录商户当前可提现余额与待结算交易。

### Database Check

库 `dpm`：

- `t_dpm_outer_account_sub_detail`
- `t_dpm_outer_account_subset`

## 对账单 (Statements)

商户对账单包含：交易对账单、结算对账单；由每日凌晨定时 JOB 批量生成。

### Database Check

库 `statementii`：

- `t_statement_transaction`
- `t_statement_settlement`
- `t_statement_balance`
- `t_statement_subscribe`

## 线下业务 (Offline Business)

包含两个环节：

1. 控台页面：设备申请与激活管理
2. BMOC 审批：`Basis--merchant => Device Approval`

### Database Check

| Database | Table |
|---|---|
| merchant | t_store |
| device | t_device_apply_order |
| device | t_active_code |
| device | t_merchant_device |
| device | t_device_key |
| device | t_destroyed_device |

## 商户设置 (Merchant Settings)

维护商户基本信息、绑卡、员工与角色、结算配置等。

### Database Check

| Database | Table | Field Check |
|---|---|---|
| merchant | t_merchant | |
| merchant | t_binding_card_apply_info | |
| merchant | t_staff | |
| merchant | t_staff_role | |
| statementii | t_settlement_config | Merchant Settlement Configuration：Reserved Amount, Minimum Withdrawal Amount |

## 相关参考

- 控台总览与导航：[[merchant-portal-overview]]
- 入驻所涉服务与组件：[[merchant-onboarding-service-map]]
- 入驻库表全量影响范围：[[merchant-onboarding-database-scope]]
