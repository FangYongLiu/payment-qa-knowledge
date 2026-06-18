---
title: PayBy核心系统简介
domain: payby-core-systems
kind: wiki_page
slug: payby-core-systems-overview
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:tester/124289174
tags: []
---

# PayBy核心系统简介

本页对 PayBy 内部业务系统与核心支付系统做整体介绍，便于建立全局认知。详见 [[domain_payby_core_systems]]。

## 主要内部业务系统

| 系统 | 功能简介 |
|---|---|
| tradeii | 交易服务（下单、支付、退款等）。交易类型：收单、红包；支付类型：余额、快捷、网银。 |
| deposit | 充值交易。支付方式：绑卡支付（使用已绑定的卡支付）、快捷支付（绑卡功能+支付）、网银、确定性入款等。 |
| foundout | 出款交易，例如提现。出款至银行卡（账户的绑定卡或指定卡信息）。 |

## 核心系统

登录账号：dev/dev

| 系统 | 功能简介 |
|---|---|
| PFS | 支付前置，给 PAYMENT 下达处理指令。 |
| PAYMENT | 支付引擎，根据 PFS 指令做事，与 CMF、DPM 打交道。 |
| CMF | 资金渠道管理。管理渠道配置、路由渠道，系统与外部渠道间的桥梁。 |
| DPM | 储值。变更账户余额、记账相关。 |
| MA | 会员系统。主要负责会员状态、基本信息。 |
| GRC | 风控系统。 |
| CGS | APP 的网关。 |
| SGS | 对外网关。 |

相关导航：21-pfs-支付前置、22-payment-支付引擎、b-cmf、31-dpm-储值、member-会员服务。

## 系统/模块负责人

- gp005_member 会员 — Meimei.Huang
- gp047_ppcenter 产品 — Meimei.Huang
- gp209_aml 反洗钱 — Dewen.liu
- gp149_vis 虚拟 IBAN — Qian.Wang
- gp004_dpm 会员账户 — Cong.Zhou
- gp123_tradeii — Zhibin.Liu、Yu.Tang
- gp006_payment — Dewen.Li
- gp007_cmf — Hefei.Zhang、Guoyou.Ma
- gp004_dpm — Yongxing.Cao
- gp193_cashierii — Zhibin.Liu
- gp079_grc — Dewen.Li
- gp012_fundout — Yu.Tang
