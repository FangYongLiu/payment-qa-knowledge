---
title: KYC 渠道总览
domain: kyc
kind: wiki_page
slug: kyc-channel-overview
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:d0566748-c0ac-4c63-8c99-c948348f3481
tags: []
related_services:
  - svc_kyc
  - svc_kyc_service
  - svc_remittance
---

# KYC 渠道总览

KYC（Know Your Customer）是用户在 Botim App 内进行任何资金类操作前必须完成的身份验证流程，目前支持 UAEKYC、UAE Pass、Passport 三个渠道，分别面向不同证件持有人群。相关业务域见 [[domain_kyc]]。

## 什么是 KYC

- 用户进入 Botim App 后，必须先完成 KYC 身份验证，才能执行任何与资金相关的交易（top-up、transfer、remittance 等）。
- KYC 可通过多个**渠道（channel）**完成；用户走哪个渠道，取决于其持有的证件类型以及自身选择的验证方式。

## 三个验证渠道对比

| Channel | Document | Underlying provider | Who uses it | Status |
|---|---|---|---|---|
| UAEKYC | Emirates ID (EID) | Official UAE API | 大多数用户（primary channel，主渠道） | ACTIVE |
| UAE Pass | EID via the UAE Pass app | UAE Pass（政府数字身份） | 偏好通过 UAE Pass 完成验证的用户 | ACTIVE |
| Passport | Passport | Signzy | 没有 EID 的 WPS workers | ACTIVE |

## 文档使用方式

本页是 KYC 文档的入口；新人（例如刚加入团队的 QA）应先阅读本页，再按自身用例打开对应渠道的子页面。

每个渠道都有独立的自包含文档，描述：
- 端到端（end-to-end）流程；
- 各步骤对应的数据库变更；
- 审计分支（audit branch）；
- 该渠道特有的业务规则。

三个子页面（作为本总览的 child pages）：

- **UAEKYC — EID KYC Knowledge Base**（含 Renew 续期流程）
- **UAE Pass — EID Verification via UAE Pass**
- **Passport — Passport KYC via Signzy**
