---
id: domain_acquiring
object_type: Domain
name: acquiring
aliases: [收单, 收单渠道, 渠道, qpay, channel]
domain: acquiring
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-24'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: [acquiring, 收单, 渠道, qpay]
related_services: [svc_qpay_ni_channel, svc_qpay_nipos, svc_qpay_niboarding, svc_qpay_installment, svc_qpay_npss, svc_qpay_fsii, svc_qpay_fs, svc_qpay_aplus, svc_qpay_pl_channel, svc_qpay_enbd, svc_qpay_klip, svc_qpay_mcii, svc_qpay_lean, svc_qpay_cko, svc_qpay_mpgs, svc_qpay_zand, svc_qpay_nisocket]
---

# acquiring(收单 / QPay 渠道)

> 业务域总览。QPay 收单渠道业务线(各第三方收单处理器接入)。域 lead 待指定。
> 命名:取 `acquiring`(收单);如需改为 `channel` 等告知。

## 概述
Acquiring 收单渠道域:QPay 系列收单渠道接入(NI/CKO/MPGS/ENBD/Zand/Lean/Klip 等第三方
收单处理器)与收单核心(qpay-mcii/fs/fsii)。此前在 payment-tools,现拆出为独立收单渠道域。

## 覆盖范围(payment-tools 迁入)
- 收单核心:qpay-mcii、qpay-fs、qpay-fsii
- 渠道接入:qpay-pl-channel、qpay-installment、qpay-ni-channel、qpay-klip、qpay-cko、
  qpay-aplus、qpay-lean、qpay-nipos、qpay-nisocket、qpay-niboarding、qpay-mpgs、
  qpay-enbd、qpay-npss、qpay-zand

## QA 关注点
- 待补。