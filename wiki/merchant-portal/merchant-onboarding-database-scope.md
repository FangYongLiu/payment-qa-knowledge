---
title: 商户入驻数据库影响范围
domain: merchant-portal
kind: wiki_page
slug: merchant-onboarding-database-scope
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/997785804
tags: []
---

# 商户入驻数据库影响范围

本页汇总商户入驻流程在各业务库中涉及的表清单及用途，便于 QA 在数据校验时定位关键落库点。完整入驻流程见 [[flow_merchant_onboarding]]，相关服务/组件见 [[merchant-onboarding-service-map]]，数据库连接方式见 [[merchant-portal-env-access-guide]]。

## 数据库账号权限

QA 库账号默认开通以下权限：

- `SELECT` – 查询数据
- `INSERT` – 插入数据
- `UPDATE` – 修改数据
- `DELETE` – 删除数据

连接时需选择具体的数据库名（例如 `merchantuser`）。

## Merchant 库

商户主域，存储商户主体、地址、合作方、业务开通、管理员、收单信息及员工等。

| Table | Purpose |
|---|---|
| `t_merchant_creation_order` | Merchant creation order（入驻申请单） |
| `t_merchant` | Merchant basic info |
| `t_merchant_address` | Merchant addresses |
| `t_partner` | Partner relationship |
| `t_binding_card_apply_info` | Binding card info |
| `t_merchant_biz_open` | Enabled business types |
| `t_biz_admin_info` | Business administrators |
| `t_merchant_acquire_info` | Acquire service info |
| `t_staff` | Merchant staff |
| `t_staff_role` | Staff role mapping |

## Member 库

承载会员身份、账户与受益人卡信息，提供下游使用的 Member ID。

| Table | Purpose |
|---|---|
| `tm_member` | Member info |
| `tm_member_identity` | Member identity |
| `tr_member_account` | Member account |
| `tr_beneficiary_info` | Beneficiary card |

## Ppcenter 库

支付产品申请与已激活产品记录。详细申请流程见 [[flow_acquire_product_application]]。

| Table | Purpose |
|---|---|
| `t_product_apply_order` | Payment product apply record |
| `t_merchant_product_order` | Merchant actived product |

## Dpm 库

商户账户体系相关。

| Table | Purpose |
|---|---|
| `t_dpm_outer_account_subset` | All Account |
| `t_dpm_account_crl_def` | Account Type |

## Statementii 库

结算配置。

| Table | Purpose |
|---|---|
| `t_settlement_config` | settlement config |

## Contract 库

入驻成功后生成的合同。

| Table | Purpose |
|---|---|
| `t_contract` | contract |

## Vis 库

虚拟 IBAN 账户（用于 IBAN Top up）。

| Table | Purpose |
|---|---|
| `t_virtual_account` | virtual account (Iban Top up) |

## QA 校验提示

- 入驻为跨系统流程，需确认上述各库的关键表均有对应记录后，商户方可视为可用。
- 校验顺序建议沿入驻链路：Merchant → Member → Ppcenter → Dpm → Statementii → Contract → Vis。
- 商户入驻完成后的产品申请、交易、账户、对账单等控台功能涉及的库表，参见 [[acquire-merchant-console-guide]]。

</br>

> 相关页面：[[merchant-portal-overview]] · [[merchant-onboarding-flow]]
