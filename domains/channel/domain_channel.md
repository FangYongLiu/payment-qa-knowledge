---
id: domain_channel
object_type: Domain
name: channel
aliases: [渠道, 收单渠道, qpay, 第三方处理器]
domain: channel
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-24'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: [channel, 渠道, qpay, 收单渠道]
related_services: [svc_qpay_ni_channel, svc_qpay_nipos, svc_qpay_niboarding, svc_qpay_installment, svc_qpay_npss, svc_qpay_fsii, svc_qpay_fs, svc_qpay_aplus, svc_qpay_pl_channel, svc_qpay_enbd, svc_qpay_klip, svc_qpay_mcii, svc_qpay_lean, svc_qpay_cko, svc_qpay_mpgs, svc_qpay_zand, svc_qpay_nisocket]
---

# channel(渠道 / QPay 第三方处理器)

> 业务域总览。QPay 系列渠道接入(各第三方收单/支付处理器)。域 lead 待指定。
> 注:「收单(acquiring)」作为 online-business 的 subdomain;本域专指渠道接入实现。

## 概述
Channel 渠道域:QPay 系列渠道接入(NI/CKO/MPGS/ENBD/Zand/Lean/Klip 等第三方处理器)
与渠道核心(qpay-mcii/fs/fsii)。从 payment-tools 拆出为独立渠道域。

## 覆盖范围(payment-tools 迁入)
- 渠道核心:qpay-mcii、qpay-fs、qpay-fsii
- 渠道接入:qpay-pl-channel、qpay-installment、qpay-ni-channel、qpay-klip、qpay-cko、
  qpay-aplus、qpay-lean、qpay-nipos、qpay-nisocket、qpay-niboarding、qpay-mpgs、
  qpay-enbd、qpay-npss、qpay-zand

## QA 关注点
- 待补。
