---
id: domain_kyc
object_type: Domain
domain: kyc
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-19'
source_type: wiki
source_ref: wiki:d0566748-c0ac-4c63-8c99-c948348f3481
tags:
- kyc
- 身份验证
subdomain: null
module: null
sensitivity: normal
name: KYC身份验证业务域
aliases:
- KYC
- Know Your Customer
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 概述
KYC (Know Your Customer) 是 Botim App 用户在进行任何资金相关交易（top-up、transfer、remittance 等）之前必须完成的身份验证业务域。用户进入 Botim App 后，需要先通过 KYC 才能开通资金类功能。KYC 可通过多个渠道（channel）完成，具体走哪个渠道取决于用户持有的证件类型以及其选择的验证方式。

## 覆盖范围
本业务域覆盖以下三个 ACTIVE 渠道：

- **UAEKYC**：基于 Emirates ID (EID)，底层走官方 UAE API，是大多数用户使用的主渠道（primary channel）。
- **UAE Pass**：基于 EID，通过 UAE Pass App 完成；底层 provider 为 UAE Pass（政府数字身份）；面向偏好使用 UAE Pass 验证的用户。
- **Passport**：基于护照（Passport），底层 provider 为 Signzy；面向没有 EID 的 WPS workers。

## 关键服务/流程
每个渠道都有独立的 end-to-end 流程文档，包含各步骤的数据库变更、审计分支（audit branch）以及该渠道特有的规则：

- UAEKYC — EID KYC Knowledge Base（含 Renew 流程）
- UAE Pass — EID Verification via UAE Pass
- Passport — Passport KYC via Signzy

详见 [[kyc-channel-overview]]。

## QA 关注点
- 入门 QA 应先阅读本 Overview，再根据具体 case 打开对应的 channel-specific 页面。
- 区分用户走哪个 channel 的判定依据：所持证件类型（EID vs Passport）以及用户选择的验证方式（官方 UAE API、UAE Pass、Signzy）。
- 注意 KYC 是资金类操作的前置条件，验证未完成则不能进行 top-up/transfer/remittance。
- 三个 channel 当前状态均为 ACTIVE，QA 需分别覆盖。
