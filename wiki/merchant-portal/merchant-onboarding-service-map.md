---
title: 商户入驻相关服务与组件清单
domain: merchant-portal
kind: wiki_page
slug: merchant-onboarding-service-map
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/997785804
tags: []
---

# 商户入驻相关服务与组件清单

本页汇总商户入驻链路涉及的微服务/前端应用、各自职责与负责人，作为排查与协作的索引。完整流程见 [[flow_merchant_onboarding]]，数据库影响范围见 [[merchant-onboarding-database-scope]]。

## 服务职责说明

入驻是跨系统流程，所有服务全部成功后商户才可用。

| Service | 职责 |
|---|---|
| Member | 全系统中央用户身份服务，管理个人/企业会员账户，提供下游使用的 Member ID |
| Merchant | 商户域服务，负责商户档案、入驻状态、商户–会员关系与生命周期 |
| Basis | 核心基础服务，处理账户启用、产品激活、运营审核决策与内部核心配置 |
| AML | 反洗钱服务，对商户与证照信息进行合规与风险筛查；AML 失败将阻断商户激活 |
| VIS | 虚拟 IBAN 服务，负责创建与管理虚拟 IBAN 账户及对外集成 |
| Billing | 账务/计费服务，负责计费账户创建、订单初始化与结算配置 |
| Contract | 合同管理服务，入驻成功后生成与管理商户合同 |
| Unified Portal | 商户注册与入驻提交的前端入口 |

## 服务应用与负责人

入驻链路涉及的应用与 Owner：

| Service | 说明 | Owner |
|---|---|---|
| gp251_unified-merchant-portal | Merchant Portal | Wang01.Kai |
| gp048_hive-merchant-console | Acquire console frontend | Wang01.Kai |
| gp045_merchant-console-frontend | merchant-console-frontend | Arpit Kumar |
| gp044_merchant | Merchant Core service | Chahid Arid |
| gp161_basis-merchant | Business Operations Backend Management | Chahid Arid |
| gp107_contract | Merchant Contract | Chahid Arid |
| gp134_statementii | Merchant statement | Shuo.Wang |
| gp005_member | System Member | Yadong.Lu |
| gp047_ppcenter | Payment Product center | Yadong Lu |
| gp209_aml | Anti-money laundering | Dewen.li / Chao Li |
| gp149_vis | Virtual IBAN | Qian.Wang |
| gp004_dpm | Savings Account | Cong.Zhou |
| gp123_tradeii | Trading Core | Yu.Tang / Yongxing.Cao |
| gp006_payment | Payment services | Dewen.li |
| gp007_cmf | Channel Management | Hefei.Zhang / Guoyou.Ma |

## 前端入口与后台审核

- 注册/入驻前端：`gp251_unified-merchant-portal`（Unified Portal），承担注册、登录与入驻表单提交。详见 [[merchant-portal-overview]] 与 [[merchant-onboarding-flow]]。
- 收单商户控台前端：`gp048_hive-merchant-console`、`gp045_merchant-console-frontend`，用于产品申请、交易/账户/对账单查询、线下设备等。详见 [[acquire-merchant-console-guide]]。
- 后台审核入口：BMOC（由 `gp161_basis-merchant` 承载），路径 `Basis Merchant => Business => Merchant => Merchant Onboarding`，完成 AML Risk Calculate 与 KYB Approval。

## 关联数据与基础设施

- 各服务对应数据库与表的清单参见 [[merchant-onboarding-database-scope]]。
- DB / Redis / Kibana 的访问方式参见 [[merchant-portal-env-access-guide]]。
- 收单产品申请与审核的服务交互参见 [[flow_acquire_product_application]]。
