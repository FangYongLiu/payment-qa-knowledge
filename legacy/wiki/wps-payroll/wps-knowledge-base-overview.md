---
title: WPS知识库总览
domain: wps-payroll
kind: wiki_page
slug: wps-knowledge-base-overview
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/2272428082
tags: []
---

# WPS知识库总览

WPS（Wage Protection System）是面向阿联酋的薪资发放产品；本页提供产品定义、文档划分、端到端旅程串联与入门导航，帮助新成员快速定位需要阅读的文档。

## 什么是 WPS

- **WPS（Wage Protection System）**：阿联酋员工薪资发放平台。
- 企业（Corporate）完成入驻、登记员工、发放薪资。
- 发放路径有两种：
  - 通过阿联酋央行（CBUAE）的 WPS 文件交换体系；
  - 直接转账（Direct Transfer）。
- 通过 **Botim Wallet** 发薪的员工会收到一张实体 **Botim Payroll Card**，并在 Botim App 中激活。

## 知识库文档划分

知识库分成两份文档，按需查阅：

| 文档 | 覆盖范围 | 何时阅读 |
|---|---|---|
| **WPS System — Knowledge Base** | 企业侧端到端薪资产品：公司注册、invoice/billing 配置、add employee、create payroll（WPS 与 Direct Transfer）、WPS 门户、PAF 类型公司 | 需要了解企业入驻、员工登记、发放流程、相关 DB 表/状态、或 YSE / 央行文件交换 |
| **Botim Payroll Card — Activation & Card Management** | 员工侧卡片生命周期：发卡、激活（EID vs Passport）、QR/CVV/proxy 获取、YSE 卡状态协调、replace、close | 需要了解员工在 Botim App 中如何激活/管理薪资卡，或排查卡数据与状态问题 |

## 端到端旅程（两份文档如何衔接）

1. **Company onboarding** — 企业在商户门户注册，开通 WPS 服务，选择公司类型（WPS-Mainland / Listed LRAs / Non-Listed LRAs / PDC），在 Basis 审核通过，注册到 YSE，获得 IBAN。（WPS System §2）
2. **Billing setup** — 任何计费操作前，员工在 Basis 配置发票模式（**Pay Now** 或 **Pay Monthly**）。（WPS System §3）
3. **Add employee** — 通过 **EID** 或 **Passport** 登记员工，类型为 **Botim Wallet** 或 **Bank Account**；在 Basis 审核，通过 CSPREG 同步到 YSE；Botim-wallet 员工随后通过 YSE-WPSCSR 发卡。（WPS System §4）
4. **Card issuance → activation** — 卡片到达后带印刷 QR 码；员工在 Botim App 完成 KYC，YSE 将卡片置为可激活状态，员工激活（EID：按钮或 QR；Passport：QR + Passport KYC）。（Payroll Card §2–§6）
   - KYC 本身属于独立的 KYC 知识库（UAEKYC / UAE Pass / Passport）。
5. **Create payroll** — 通过 **WPS**（央行文件交换：SIF/PIF/PRC/DIF）或 **Direct Transfer** 发薪，门户审批，由 YSE/TradeII 执行。（WPS System §5）
6. **Ongoing management** — 公司通过 WPS 门户自助管理（Dashboard、Payrolls、Employees、Invoice、Reports、Roles）；员工管理卡片（replace、statement、close）。（WPS System §6，Payroll Card §7–§8）

## 两个需要分清的变体

- **SIF vs PAF**：由 `bps.t_corporate` 的 `process_type` 区分。SIF 是默认的端到端产品（门户发薪、invoice 模块）；PAF 只把我们当作发放通道——无门户发薪、无 invoice 模块、线下结算、YSE 驱动发薪、含母/子公司结构。详见 [[wps-sif-vs-paf]]。
- **EID vs Passport employees**：Passport 用户始终是 Botim-card 用户，初始状态为 `KYCVerification`，且卡片激活时**必须走 QR-code 路径**才能到达 Passport KYC 选项；EID 用户可通过按钮或 QR 激活。

## 入门导航

- 想先了解参与方与系统职责 → [[wps-key-actors]]
- 想知道数据存在哪些表 → [[wps-data-map]]
- 想区分 SIF 与 PAF 公司类型 → [[wps-sif-vs-paf]]
- 业务域定义 → [[domain_wps_payroll]]

## 相关知识库

- **KYC — Channel Overview**（UAEKYC / UAE Pass / Passport）：身份验证步骤，是卡片激活与资金交易的前置。其中 **Passport** 通道专门服务 WPS 工人路径。
