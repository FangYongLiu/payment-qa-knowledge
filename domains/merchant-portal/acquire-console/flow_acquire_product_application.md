---
id: flow_acquire_product_application
object_type: Flow
domain: merchant-portal
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: confluence:AQ/997785804
tags:
- acquire
- product
- bmoc
- ppcenter
subdomain: acquire-console
module: null
sensitivity: normal
name: 收单支付产品申请与审核流程
aliases: []
related_services:
- gp048_hive-merchant-console
- gp047_ppcenter
- gp161_basis-merchant
related_tables:
- ppcenter.t_product_apply_order
- ppcenter.t_product_apply_info
- ppcenter.t_merchant_product_order
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 概述
商户在收单商户控台 (Acquire Merchant Console) 申请支付产品，或由业务团队在 BMOC 系统替商户开通产品，最终都需要在 BMOC 进入审核流程，审核通过后产品才会被激活。

前置条件：
- 商户已经在 Botim Merchant Portal 注册，并通过 Merchant Portal 登录后选择 `Payment` (即 Merchant Acquire Service) 业务类型。
- 已完成 [[flow_merchant_onboarding]] 中的 KYB Approval，商户状态正常。

## 步骤(跨系统)
### Method 1：商户控台主动申请
1. 商户登录 Acquire Merchant Console，通过菜单 `Apply for payment products` 主动申请所需产品。
2. 申请提交后进入 BMOC 系统等待审核。
3. BMOC 审核路径：`Basis-merchant => General => Product Audit => Apply Audit`。
4. 审核通过后，产品状态被激活。

### Method 2：BMOC 系统替商户开通
1. 业务团队在 BMOC 进入：`Basis-merchant => General => ProductOpenMgt => Merchant Open Product` 直接为商户申请开通产品。
2. 在 `Basis-merchant => General => Product Audit => Apply Audit` 完成审核。
3. 审核通过后产品被激活。

### 支持的产品与系统产品码
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

## 涉及服务/表
涉及服务：
- `gp048_hive-merchant-console` (Acquire console frontend)
- `gp047_ppcenter` (Payment Product center)
- `gp161_basis-merchant` (Business Operations Backend Management / BMOC)

涉及数据库与表 (database = `ppcenter`)：
- `t_product_apply_order` — 产品申请单
- `t_product_apply_info` — 产品申请信息
- `t_merchant_product_order` — 商户已激活产品

## 校验点
- `ppcenter.t_product_apply_order.status = S`（审核通过状态）。
- `ppcenter.t_product_apply_info` 中存在对应申请记录。
- 审核通过后 `ppcenter.t_merchant_product_order` 中生成商户已激活产品记录，且 `System Product Code` 与所申请产品一致。
- 在 BMOC `Apply Audit` 菜单中确认申请单已完成审核动作。
