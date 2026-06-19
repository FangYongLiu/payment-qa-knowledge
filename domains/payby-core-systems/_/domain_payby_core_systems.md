---
id: domain_payby_core_systems
object_type: Domain
domain: acquire-transaction
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: confluence:tester/124289174
tags:
- 核心系统
- 支付平台
- 内部业务系统
subdomain: null
module: null
sensitivity: normal
name: PayBy核心系统域
aliases: []
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 概述

PayBy核心系统域涵盖PayBy支付平台的内部业务系统与核心支付系统两大类，构成整体业务域。内部业务系统主要承载交易（收单、红包）、充值、出款等业务流程；核心系统则负责支付指令下达、支付引擎处理、资金渠道管理、储值记账、会员管理、风控、网关等基础能力。

## 覆盖范围

**主要内部业务系统：**
- **tradeii**：交易服务（下单、支付、退款等）。交易类型主要包含：收单、红包。支付类型支持：余额、快捷、网银。
- **deposit**：充值交易。支付方式：绑卡支付（使用已绑定的卡支付）、快捷支付（绑卡功能+支付）、网银、确定性入款等。
- **foundout**：出款交易，比如提现。出款至银行卡（账户的绑定卡或指定卡信息）。

**核心系统**（登录：dev/dev）：
- **PFS**：支付前置，给PAYMENT下达处理指令。
- **PAYMENT**：支付引擎，根据PFS指令做事，与CMF、DPM打交道。
- **CMF**：资金渠道管理。管理渠道配置，路由渠道，系统与外部渠道间的桥梁。
- **DPM**：储值。变更账户余额、记账相关。
- **MA**：会员系统。主要与会员状态，基本信息相关。
- **GRC**：风控系统。
- **CGS**：APP的网关。
- **SGS**：对外网关。

**相关代码组（gp）映射：**
- gp005_member 会员
- gp047_ppcenter 产品
- gp209_aml 反洗钱
- gp149_vis 虚拟IBAN
- gp004_dpm 会员账户 / gp004_dpm
- gp123_tradeii
- gp006_payment
- gp007_cmf
- gp193_cashierii
- gp079_grc
- gp012_fundout

## 关键服务/流程

- **交易类**：tradeii 承载收单、红包等交易；支持余额、快捷、网银多种支付类型。
- **充值类**：deposit 处理绑卡支付、快捷支付、网银、确定性入款。
- **出款类**：foundout 处理提现至银行卡（绑定卡或指定卡）。
- **支付主链路**：PFS → PAYMENT → CMF（外部渠道）/ DPM（账户余额与记账）。
- **支撑服务**：MA（会员）、GRC（风控）、CGS（APP网关）、SGS（对外网关）。

## QA 关注点

- 内部业务系统（tradeii/deposit/foundout）与核心系统（PFS/PAYMENT/CMF/DPM）之间的指令与资金流转衔接。
- 不同支付类型（余额、快捷、网银、绑卡、确定性入款）在交易/充值场景的覆盖。
- 出款链路中绑定卡与指定卡两种卡信息来源的差异。
- 网关（CGS 对内 APP、SGS 对外）与风控（GRC）、会员（MA）在交易链路上的介入点。
- 各核心系统对应代码组（gp 系列）与 owner 的对应关系，便于问题定位。
