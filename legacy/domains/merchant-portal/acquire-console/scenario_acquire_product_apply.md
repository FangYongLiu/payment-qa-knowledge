---
id: scn_acquire_product_apply
object_type: Scenario
domain: merchant-portal
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: wiki:fa5361b9-9768-4302-b8dc-f2dd9cc50451
tags:
- acquire
- product-apply
- bmoc
- ppcenter
subdomain: acquire-console
module: product-apply
sensitivity: normal
name: 收单商户支付产品申请测试场景
aliases: []
related_services:
- gp048_hive-merchant-console
- gp161_basis-merchant
- gp047_ppcenter
related_tables:
- ppcenter.t_product_apply_order
- ppcenter.t_product_apply_info
- ppcenter.t_merchant_product_order
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 触发/入口
收单商户(Payment 业务类型)在控台申请并开通支付产品，支持两种方式：

- Method 1：商户在 Acquire Merchant Console 通过控台菜单主动申请产品，提交后进入 BMOC 审核。
- Method 2：业务团队在 BMOC 系统直接为商户开通产品。
  - Apply 菜单路径：`Basis-merchant => General => ProductOpenMgt => Merchant Open Product`
  - Audit 菜单路径：`Basis-merchant => General => Product Audit => Apply Audit`

## 前置条件
- 已完成 Botim Merchant 注册(参考 [[merchant-onboarding-flow]])。
- 通过 Merchant Portal 登录，业务类型选择 `Payment`(即 Merchant Acquire Service)。
- 商户 Onboarding 状态已通过 BMOC 审核(AML Risk Calculate + KYB Approval)。

## 操作步骤
### Method 1：控台自助申请
1. 登录收单商户控台 [[acquire-merchant-console]]，进入产品申请菜单。
2. 选择需要申请的支付产品并提交。
3. 业务运营在 BMOC 系统进行审核。

### Method 2：BMOC 后台开通
1. 业务团队登录 BMOC，进入 `Basis-merchant => General => ProductOpenMgt => Merchant Open Product` 为指定商户发起开通申请。
2. 在 `Basis-merchant => General => Product Audit => Apply Audit` 完成审核。

### 支持的产品与产品码
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

## DB 校验点
库：`ppcenter`

| Table | Field Check |
| --- | --- |
| `t_product_apply_order` | `status = S` |
| `t_product_apply_info` | 产品申请明细记录存在 |
| `t_merchant_product_order` | 商户已激活产品记录存在 |

## 预期结果
- BMOC 审核通过后，`ppcenter.t_product_apply_order.status` 变为 `S`(Success)。
- `t_product_apply_info` 记录该笔申请的产品明细。
- `t_merchant_product_order` 写入商户已开通产品记录，对应所申请的 System Product Code。
- 商户在收单控台可看到对应支付产品已开通，可继续进行 API 接入与交易。
