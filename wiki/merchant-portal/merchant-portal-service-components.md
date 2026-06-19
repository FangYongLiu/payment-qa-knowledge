---
title: 商户控台服务应用清单
domain: merchant-portal
kind: wiki_page
slug: merchant-portal-service-components
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:5c621189-7c84-418e-ae94-d862f23a7480
tags: []
---

# 商户控台服务应用清单

本页汇总商户控台（Merchant Portal）业务域涉及的微服务组件清单、各服务职责说明及对应 Owner，便于在测试和问题排查时快速定位负责人。

## 服务职责说明

商户 Onboarding 是跨系统流程，所有相关服务均成功后商户才可用。各核心服务职责如下：

- **Member**：全系统中央用户身份服务，管理个人/企业会员账户，向下游提供 `Member ID`。
- **Merchant**：商户域服务，负责商户档案、Onboarding 状态、商户–会员关系、商户生命周期管理。
- **Basis**：核心基础服务，处理账户启用、产品激活、运营审核决策、内部核心配置。
- **AML**：反洗钱服务，对商户与执照信息做合规与风险筛查；AML 失败将阻断商户激活。
- **VIS**：Virtual IBAN 服务，负责虚拟 IBAN 账户的创建、管理与外部对接。
- **Billing**：计费与账务服务，负责计费账户创建、订单初始化和结算配置。
- **Contract**：合同管理服务，Onboarding 成功后生成与管理商户合同。
- **Unified Portal**：商户注册与 Onboarding 提交的前端入口。

相关流程参见 [[merchant-onboarding-flow]]，数据落库范围参见 [[merchant-onboarding-database-scope]]。

## 服务应用 Owner 清单

| Service Name | 说明 | Owner | 备注 |
|---|---|---|---|
| gp251_unified-merchant-portal | Merchant Portal | Wang01.Kai | |
| gp048_hive-merchant-console | Acquire console frontend | Wang01.Kai | |
| gp045_merchant-console-frontend | merchant-console-frontend | Arpit Kumar | |
| gp044_merchant | Merchant Core service | Chahid Arid | |
| gp161_basis-merchant | Business Operations Backend Management | Chahid Arid | |
| gp107_contract | Merchant Contract | Chahid Arid | |
| gp134_statementii | Merchant statement | Shuo.Wang | |
| gp005_member | System Member | Yadong.Lu | |
| gp047_ppcenter | Payment Product center | Yadong.Lu | |
| gp209_aml | Anti-money laundering | Dewen.li / Chao Li | |
| gp149_vis | Virtual IBAN | Qian.Wang | |
| gp004_dpm | Savings Account | Cong.Zhou | |
| gp123_tradeii | Trading Core | Yu.Tang / Yongxing.Cao | |
| gp006_payment | Payment services | Dewen.li | |
| gp007_cmf | Channel Management | Hefei.Zhang / Guoyou.Ma | |

## 前后端组件归属

- **商户前台入口**：`gp251_unified-merchant-portal`（统一门户，注册/登录）。
- **收单控台前端**：`gp048_hive-merchant-console`、`gp045_merchant-console-frontend`，对应 [[acquire-merchant-console]] 中的页面功能。
- **商户核心后端**：`gp044_merchant`（Merchant 域）+ `gp161_basis-merchant`（运营审核 BMOC）。
- **支付产品**：`gp047_ppcenter` 负责 Apply / Activate 流程。
- **账户与交易**：`gp004_dpm`（账户）、`gp123_tradeii`（交易核心）、`gp006_payment`、`gp007_cmf`（渠道）。
- **风控与合规**：`gp209_aml`。
- **虚拟账户**：`gp149_vis`（VAM/IBAN Top up）。
- **合同与对账单**：`gp107_contract`、`gp134_statementii`。

## 系统组件分类与依赖

平台底层组件按归属与职责划分为以下几类（来源：System Components 架构图）：

### 组件分类

- **内部应用（Internal Application）**：`ues`、`ufs`。
- **内部管理（Internal Management）**：内部运维管理类组件。
- **内部 jar 组件（Internal jar Component）**：业务应用统一引入的基础 starter 与工具包：
  - `beacon`、`basic-lang`、`basic-util(dep)`、`pmock`、`ues-client`、`sequence-util`
  - `monitor-starter`、`mq-stater`、`dubbo-starter`、`job-starter`、`redis-starter`、`mysql-starter`
  - `cobarclient`
- **第三方应用（Third-party Application）**：`spring-cloud-config`、`nacos`、`rabbit-mq`、`zookeeper`、`redis`、`mysql`、`gitlab`、`阿里云（Aliyun）`。
- **第三方管理（Third-party Management）**：`gitlab`、`spring-boot-admin`、`dubbo-admin`、`elasticjob-console`。

### 关键依赖关系

- `beacon` → `basic-lang`
- `monitor-starter` → `spring-cloud-config`、`nacos`
- `spring-cloud-config` → `gitlab`
- `spring-boot-admin` → `nacos`
- `mq-stater` → `rabbit-mq`
- `dubbo-starter` → `zookeeper`
- `job-starter` → `zookeeper`
- `dubbo-admin` → `zookeeper`
- `elasticjob-console` → `zookeeper`
- `redis-starter` → `redis`
- `ues-client` → `ues`

> 配置中心走 `spring-cloud-config` + `gitlab`；服务注册/调度走 `zookeeper`（Dubbo、ElasticJob）；监控与运维管理（spring-boot-admin、monitor-starter）依赖 `nacos`。

## 相关链接

- 总览与功能介绍：[[merchant-portal-overview]]
- 收单商户控台功能页：[[acquire-merchant-console]]
- 日志/Redis/DB 接入方式：[[qa-infra-access-guide]]
