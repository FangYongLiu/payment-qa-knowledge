---
title: 商户Onboarding数据库影响范围
domain: merchant-portal
kind: wiki_page
slug: merchant-onboarding-database-scope
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:fa5361b9-9768-4302-b8dc-f2dd9cc50451
tags: []
---

# 商户Onboarding数据库影响范围

本页梳理商户 Onboarding 流程在各业务库中所触达的库与表清单，便于在 [[flow_merchant_onboarding]] 与 [[scn_acquire_product_apply]] 等场景下做数据校验。数据库连接方式与权限参考 [[qa-infra-access-guide]]。

## 概览

- Onboarding 是跨系统流程，落库分布在 7 个库：`Merchant` / `Member` / `Ppcenter` / `Dpm` / `Statementii` / `Contract` / `Vis`。
- QA 账号默认权限：`SELECT` / `INSERT` / `UPDATE` / `DELETE`。
- 连接库时需指定具体库名（例如 `merchantuser`）。
- 业务流程与服务职责见 [[merchant-onboarding-flow]]，对应服务清单见 [[merchant-portal-service-components]]。

## Merchant 库

商户主域，记录注册单、商户主体、地址、绑卡、业务开通与员工信息。

| Table | Purpose |
|---|---|
| t_merchant_creation_order | Merchant creation order（商户创建单） |
| t_merchant | Merchant basic info |
| t_merchant_address | Merchant addresses |
| t_partner | Partner relationship |
| t_binding_card_apply_info | Binding card info |
| t_merchant_biz_open | Enabled business types |
| t_biz_admin_info | Business administrators |
| t_merchant_acquire_info | Acquire service info |
| t_staff | Merchant staff |
| t_staff_role | Staff role mapping |

## Member 库

中心化用户身份域，提供下游使用的 `Member ID`。

| Table | Purpose |
|---|---|
| tm_member | Member info |
| tm_member_identity | Member identity |
| tr_member_account | Member account |
| tr_beneficiary_info | Beneficiary card |

## Ppcenter 库

支付产品中心，记录产品申请与已开通产品。在 [[acquire-merchant-console]] 申请产品后会落到该库。

| Table | Purpose |
|---|---|
| t_product_apply_order | Payment product apply record（审核通过后 status = `S`） |
| t_merchant_product_order | Merchant actived product |

## Dpm 库

账户域（Savings Account），承载所有账户实体与账户类型定义。

| Table | Purpose |
|---|---|
| t_dpm_outer_account_subset | All Account |
| t_dpm_account_crl_def | Account Type |

## Statementii 库

结算/对账配置域。

| Table | Purpose |
|---|---|
| t_settlement_config | settlement config（结算配置） |

## Contract 库

商户合同域，Onboarding 成功后生成。

| Table | Purpose |
|---|---|
| t_contract | contract |

## Vis 库

虚拟 IBAN 域，用于 IBAN Top up 场景。

| Table | Purpose |
|---|---|
| t_virtual_account | virtual account (Iban Top up) |

## 校验建议

- 注册提交后：先核对 `Merchant.t_merchant_creation_order` 与 `t_merchant`，再看 `Member.tm_member` / `tm_member_identity` 是否生成。
- 业务类型（Payment）选择后：检查 `t_merchant_biz_open`、`t_merchant_acquire_info`、`t_biz_admin_info`。
- BMOC 完成 AML + KYB 审核后：确认 `Contract.t_contract`、`Dpm.t_dpm_outer_account_subset`、`Vis.t_virtual_account`、`Statementii.t_settlement_config` 均落数据，方可视为 Onboarding 完整成功。
- 整体回到 [[merchant-portal-overview]] 查看控台总览。
