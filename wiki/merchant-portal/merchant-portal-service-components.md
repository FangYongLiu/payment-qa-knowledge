---
title: 商户控台服务应用清单
domain: merchant-portal
kind: wiki_page
slug: merchant-portal-service-components
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:2643daf0-0884-4213-87c1-688b78a45388
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

业务服务（如本页 Owner 清单中的各 `gpXXX_*`）在底层依赖一组共享的基础组件。组件按归属分为五类：

| 类别 | 颜色标识 | 说明 |
|---|---|---|
| 内部应用 (Internal Application) | 浅蓝 | 内部自研、独立部署运行的业务/平台应用 |
| 内部管理 (Internal Management) | 浅蓝 | 内部自研的管理后台类组件 |
| 内部 jar 组件 (Internal jar component) | 橙色 | 内部维护、以 jar 形式被业务应用依赖的库/Starter |
| 第三方应用 (Third-party Application) | 浅绿 | 外部开源/商用的运行态中间件与存储 |
| 第三方管理 (Third-party Management) | 浅绿（圆角） | 外部开源的管理控制台类组件 |

### 内部 jar 组件

通用基础库与工具：

- `beacon` → 依赖 `basic-lang`
- `basic-lang`：基础语言/通用类型库
- `basic-util(dep)`：基础工具库
- `pmock`：打桩/Mock 工具
- `ues-client` → 依赖内部应用 `ues`

中间件接入 Starter（业务服务通过引入这些 Starter 接入对应中间件）：

- `monitor-starter` → `spring-cloud-config`、`nacos`
- `mq-stater` → `rabbit-mq`（并连接 `nacos`）
- `dubbo-starter` → `zookeeper`
- `job-starter` → `zookeeper`
- `redis-starter` → `redis`
- `mysql-starter` → `mysql`
- `sequence-util` → `mysql`（分布式序列）
- `cobarclient` → `mysql`（分库分表客户端）

### 内部应用

- `ues` → 依赖 `redis`、`mysql`

### 第三方应用（运行时依赖）

- `spring-cloud-config` → `gitlab`、`nacos`
- `nacos`：配置与注册中心
- `rabbit-mq`：消息队列
- `zookeeper`：协调服务（Dubbo / ElasticJob 依赖）
- `redis`：缓存
- `mysql`：关系型数据库

### 第三方管理控制台

- `spring-boot-admin` → `nacos`、`rabbit-mq`
- `dubbo-admin` → `zookeeper`
- `elasticjob-console` → `zookeeper`

> 排查思路：业务服务（Merchant、Basis、AML、VIS 等）出现中间件相关异常时，按"业务服务 → 对应 Starter（如 `redis-starter`/`mysql-starter`/`mq-stater`/`dubbo-starter`）→ 第三方组件（redis/mysql/rabbit-mq/zookeeper）"链路定位；配置类问题优先核对 `nacos` 与 `spring-cloud-config`。

## 相关链接

- 总览与功能介绍：[[merchant-portal-overview]]
- 收单商户控台功能页：[[acquire-merchant-console]]
- 日志/Redis/DB 接入方式：[[qa-infra-access-guide]]
