---
title: PayBy核心系统简介
domain: acquire-transaction
kind: wiki_page
slug: payby-core-systems-overview
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:c52f726d-c7dc-42a2-bc1a-0226402bc422
tags: []
related_services:
  - svc_aml
  - svc_cashierii
  - svc_cgs
  - svc_cmf
  - svc_deposit
  - svc_dpm_accounting
  - svc_dpm_manager
  - svc_fundout
  - svc_member
  - svc_payment
  - svc_pfs_payment
  - svc_ppcenter
  - svc_sgs
  - svc_tradeii
  - svc_vis
---

# PayBy核心系统简介

本页对 PayBy 内部业务系统与核心系统做整体概览，便于快速建立系统全貌的认知。

## 主要内部业务系统

| 系统名称 | 功能简介 |
|---------|---------|
| tradeii | 交易服务（下单、支付、退款等）。交易类型主要包含：收单、红包。支付类型支持：余额、快捷、网银。 |
| deposit | 充值交易。支付方式：绑卡支付（使用已绑定的卡支付）、快捷支付（绑卡功能+支付）、网银、确定性入款等。 |
| foundout | 出款交易，比如提现。出款至银行卡（账户的绑定卡或指定卡信息）。 |

## 核心系统

登录账号：`dev/dev`

| 系统名称 | 功能简介 | 相关导航 |
|---------|---------|---------|
| PFS | 支付前置，给 PAYMENT 下达处理指令。 | 21-pfs-支付前置 |
| PAYMENT | 支付引擎，根据 PFS 指令做事，与 CMF、DPM 打交道。 | 22-payment-支付引擎 |
| CMF | 资金渠道管理。管理渠道配置，路由渠道，系统与外部渠道间的桥梁。 | b-cmf |
| DPM | 储值。变更账户余额、记账相关。 | 31-dpm-储值 |
| MA | 会员系统。主要与会员状态、基本信息相关。 | member-会员服务 |
| GRC | 风控系统 | — |
| CGS | APP 的网关 | — |
| SGS | 对外网关 | — |

## 系统调用关系

- 业务系统（tradeii / deposit / foundout）发起业务请求。
- PFS 作为支付前置，向 PAYMENT 下达处理指令。
- PAYMENT 作为支付引擎执行处理，下游与 CMF（渠道）、DPM（账户记账）交互。
- CMF 对接外部资金渠道；DPM 负责账户余额变更与记账。
- MA 提供会员信息支撑，GRC 提供风控能力。
- CGS 承担 APP 网关，SGS 承担对外网关。

## 业务域与负责团队

| 业务域代号 | 业务域 | 负责人 |
|-----------|-------|-------|
| gp005_member | 会员 | Meimei.Huang |
| gp047_ppcenter | 产品 | Meimei.Huang |
| gp209_aml | 反洗钱 | Dewen.liu |
| gp149_vis | 虚拟IBAN | Qian.Wang |
| gp004_dpm | 会员账户 | Cong.Zhou |
| gp123_tradeii | — | Zhibin.Liu, Yu.Tang |
| gp006_payment | — | Dewen.Li |
| gp007_cmf | — | Hefei.Zhang, Guoyou.Ma |
| gp004_dpm | — | Yongxing.Cao |
| gp193_cashierii | — | Zhibin.Liu |
| gp079_grc | — | Dewen.Li |
| gp012_fundout | — | Yu.Tang |
