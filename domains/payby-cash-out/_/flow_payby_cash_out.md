---
id: flow_payby_cash_out
object_type: Flow
domain: withdraw-cash
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: confluence:tester/124289136
tags: []
subdomain: null
module: null
sensitivity: normal
name: PayBy 现金提现交易流程
aliases: []
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 概述
用户有将 PayBy 余额直接提现为现金（而非进入银行卡）的需求时，通过线下商户使用 POS 机完成现金提现交易。用户出示付款码，POS 机扫码识别后进行用户核身，商户确认无误后将等额现金交给用户，交易完成。

## 步骤(跨系统)
1. 用户出示付款码：用户在 PayBy 端生成并出示付款码。
2. POS 机扫码：商户使用 POS 机扫描用户的付款码。
3. 用户核身：对用户身份进行核验。
4. 商户确认并付现：商户确认交易信息后，将现金交付给用户。
5. 交易完成。

## 涉及服务/表
原文未提及具体服务或数据表。

## 校验点
- 用户付款码有效性（POS 机扫码识别）。
- 用户核身校验通过。
- 商户确认环节：核对后将现金交付给用户。
