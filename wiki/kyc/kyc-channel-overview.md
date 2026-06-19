---
title: KYC 渠道总览
domain: kyc
kind: wiki_page
slug: kyc-channel-overview
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/2265251857
tags: []
---

# KYC 渠道总览

本页是 KYC 文档的入口：先了解 KYC 业务概念与三种验证渠道的适用场景，再跳转到对应渠道的子页。面向新加入团队的 QA 等读者。

## 什么是 KYC

用户进入 Botim App 后，必须先完成 **KYC（Know Your Customer）身份验证**，才能执行任何与资金相关的交易（top-up、transfer、remittance 等）。

KYC 可通过多个**渠道（channel）**完成；具体走哪一条，取决于用户持有的证件以及其选择的验证方式。详见 [[domain_kyc]]。

## 渠道一览

| Channel | Document | Underlying provider | Who uses it | Status |
|---|---|---|---|---|
| UAEKYC | Emirates ID (EID) | Official UAE API | 大部分用户（主渠道） | ACTIVE |
| UAE Pass | EID via the UAE Pass app | UAE Pass（政府数字身份） | 倾向使用 UAE Pass 验证的用户 | ACTIVE |
| Passport | Passport | Signzy | 没有 EID 的 WPS workers | ACTIVE |

## 如何使用这些文档

每个渠道都有独立的子页，覆盖端到端流程、各步骤的数据库变更、审核分支以及渠道特定规则。三个渠道子页挂在本总览下：

- **UAEKYC — EID KYC Knowledge Base**（含 Renew 流程）
- **UAE Pass — EID Verification via UAE Pass**
- **Passport — Passport KYC via Signzy**

建议从本页开始，再按用户场景打开对应的渠道页。
