---
id: domain_kyc
object_type: Domain
domain: kyc
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-19'
source_type: wiki
source_ref: confluence:AQ/2265251857
tags:
- kyc
- identity-verification
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
KYC (Know Your Customer) 是 Botim App 用户进入后必须完成的身份验证流程。用户在执行任何资金相关交易（top-up、transfer、remittance 等）之前，必须先完成 KYC 身份验证。

KYC 验证可通过多个 **channels** 完成；用户走哪条 channel 取决于其持有的证件类型以及验证方式偏好。

## 覆盖范围
本业务域覆盖 Botim App 用户身份验证的全部场景，包括：

- 资金类交易前置的身份验证（top-up、transfer、remittance 等）
- 多渠道（channel）KYC 接入与流程编排
- 各渠道端到端流程、数据库状态变更、审计分支与渠道特定规则
- Renew（续期）流程（归属于 UAEKYC 渠道页）

## 关键服务/流程
KYC 业务域当前包含三个 ACTIVE 渠道：

| Channel | Document | Underlying provider | Who uses it | Status |
|---|---|---|---|---|
| UAEKYC | Emirates ID (EID) | Official UAE API | 大多数用户（主渠道） | ACTIVE |
| UAE Pass | EID via the UAE Pass app | UAE Pass (政府数字身份) | 倾向使用 UAE Pass 验证的用户 | ACTIVE |
| Passport | Passport | Signzy | 没有 EID 的 WPS workers | ACTIVE |

每个 channel 有独立的自包含文档页，描述：
- 端到端流程（end-to-end flow）
- 各步骤的数据库变更
- 审计分支（audit branch）
- 渠道特定规则（channel-specific rules）

子页面：
- UAEKYC — EID KYC Knowledge Base（含 Renew flow）
- UAE Pass — EID Verification via UAE Pass
- Passport — Passport KYC via Signzy

参考：[[kyc-channel-overview]]

## QA 关注点
- 用户进入 Botim App 后，未完成 KYC 不应能执行任何 money-related transactions（top-up / transfer / remittance）。
- 渠道选择应与用户证件类型匹配：持 EID 用户走 UAEKYC 或 UAE Pass；无 EID 的 WPS workers 走 Passport (Signzy)。
- 每个渠道都有各自的流程、DB 状态变更和审计分支，排查问题时需先确认用户走的是哪条 channel，再进入对应渠道页定位。
- UAEKYC 渠道额外覆盖 Renew 流程，需关注续期场景的状态流转。
- 文档为分层结构：Overview 为入口，channel-specific page 为详细排查依据。
