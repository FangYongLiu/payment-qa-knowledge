---
title: 商户注册来源概览
domain: merchant-management
kind: wiki_page
slug: merchant-registration-sources
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:34ef57ae-73fe-4cd4-a064-e8edfb238167
tags: []
---

# 商户注册来源概览

本页梳理商户管理业务域中商户注册的来源渠道，作为后续 Acquire / WPS 开通流程的入口说明。

## 注册来源渠道

商户注册来源共四个：

- **Unified Portal**（统一控台）
- **Agent**
- **Basis**
- **Botim**

## Unified Portal（统一控台）

统一控台是当前文档化最完整的注册入口，可作为商户进入系统的主要渠道，支持以下能力：

- 提交商户申请并开通 **Acquire** 或 **WPS** 业务
  - 申请入口接口：`/api/acquiring/permitAll/merchant/apply/add`，详见 [[api_merchant_apply_add]]
  - 开通 WPS 入口接口：`api/acquiring/secure/merchant2/bizOpen/wps`，详见 [[api_merchant_bizopen_wps]]
- 申请提交后由 **Basis** 完成审核（Acquire / WPS 审核分别推进各自落库流程）

## Agent / Basis / Botim

原文仅列出渠道名称，未展开具体接入流程；本页保留来源枚举以保证完整性，具体落库与审核细节以各业务流程文档为准。

## 后续开通流程

不同来源渠道在提交申请后，统一进入业务开通流程：

- Acquire 业务开通详见 [[merchant-acquire-onboarding-flow]] 与端到端流程 [[flow_merchant_acquire_onboarding]]
- WPS 业务开通详见 [[merchant-wps-onboarding-flow]] 与端到端流程 [[flow_merchant_wps_onboarding]]

所属业务域参见 [[domain_merchant_management]]。
