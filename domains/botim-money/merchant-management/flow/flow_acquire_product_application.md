---
id: flow_acquire_product_application
object_type: Flow
name: 收单商户控台产品申请与开通流程
aliases: [acquire product application, merchant product apply, 支付产品申请]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: 'confluence:AQ/997785804, wiki:fa5361b9'
tags: [acquire, merchant-console, product, ppcenter, device]
related_services: [svc_hive_merchant_console, svc_merchant, svc_basis_merchant, svc_ppcenter]
related_tables: []
related_scenarios: []
---

# 收单商户控台产品申请与开通流程

## 概述
商户完成入驻(见 [[flow_merchant_onboarding]])并以 `Payment`(Merchant Acquire Service)业务类型登录后，进入收单商户控台(Acquire Merchant Console)。本流程覆盖支付产品申请与开通，以及控台各功能模块(交易/账户/对账单/线下设备/商户设置)对应的库表校验点。控台前端由 [[svc_hive_merchant_console]] 承载，审核在 [[svc_basis_merchant]](BMOC)，产品中心为 [[svc_ppcenter]]。

## 步骤(跨系统)
1. 商户以 `Payment` 业务登录收单控台 —— [[svc_hive_merchant_console]]。
2. 申请支付产品(两种路径):
   - **Method 1**:商户在控台菜单主动申请产品 → 进入 BMOC 审核。
   - **Method 2**:业务团队在 BMOC 直接为商户开通。申请路径 `Basis-merchant => General => ProductOpenMgt => Merchant Open Product`;审核路径 `Basis-merchant => General => Product Audit => Apply Audit`。
3. BMOC 审核通过 —— [[svc_basis_merchant]]，产品落库 [[svc_ppcenter]]。

## 产品与 System Product Code
| Product Name | API Payment Scenarios | System Product Code |
| --- | --- | --- |
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

## 关联关系
- **经过的服务(有序)**:[[svc_hive_merchant_console]] → [[svc_basis_merchant]] → [[svc_ppcenter]] → [[svc_merchant]](= `related_services`)
- **关键场景**:结算/提现/退款的授权操作见 [[scn_merchant_settlement_withdraw_auth]]
- **环境/控台入口**:[[ref_portal_env_access]]、[[ref_bmoc_basis_merchant]]、[[ref_merchant_portal_products]]

## 控台模块与库表校验点

### 产品申请(ppcenter)
- `t_product_apply_order`(status: `S`)、`t_product_apply_info`、`t_merchant_product_order`

### 交易(Transactions)
覆盖订单处理、退款、提现、个人/银行转账、VAM 充值。
| 库 | 表 | 校验 |
| --- | --- | --- |
| acquireii | `t_acquire_order` | status: `S` |
| acquireii | `t_refund_order` | — |
| mhtfundout | `t_withdraw_order` / `t_fundout_order` / `t_fundout_bankcard_order` | — |
| deposit | `t_deposit_order` | — |

### 账户(Account)
- `dpm.t_dpm_outer_account_sub_detail`、`dpm.t_dpm_outer_account_subset`(可提现余额与在途交易)

### 对账单(Statements)
每日凌晨定时 JOB 批量生成，含交易对账单与结算对账单。
- `statementii.t_statement_transaction` / `t_statement_settlement` / `t_statement_balance` / `t_statement_subscribe`

### 线下业务(Offline Business)
控台申请激活 + BMOC `Basis--merchant => Device Approval` 审批。
- `merchant.t_store`、`device.t_device_apply_order` / `t_active_code` / `t_merchant_device` / `t_device_key` / `t_destroyed_device`(设备表对象见 [[tbl_merchant_device]])

### 商户设置(Merchant Settings)
- `merchant.t_merchant` / `t_binding_card_apply_info` / `t_staff` / `t_staff_role`
- `statementii.t_settlement_config`:结算参数 Reserved Amount、Minimum Withdrawal Amount

## 校验点
- 产品申请:`t_product_apply_order.status=S` 且 `t_merchant_product_order` 有对应记录。
- 交易:`t_acquire_order.status=S`。
- 线下设备:控台申请 + BMOC Device Approval 双侧状态一致。
