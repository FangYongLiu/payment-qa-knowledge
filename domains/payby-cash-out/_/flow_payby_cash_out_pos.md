---
id: flow_payby_cash_out_pos
object_type: Flow
domain: withdraw-cash
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: wiki:fe5f98bc-c2e2-43b6-862c-8e832eed6be0
tags: []
subdomain: null
module: null
sensitivity: normal
name: Cash Out POS提现现金流程
aliases: []
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 概述
用户有将 PayBy 余额直接提现为现金（而非进入银行卡）的需求。该流程通过用户在 POS 机出示付款码完成扫码核身，商户确认后将等额现金交付用户，实现端到端的现金提现。

## 步骤(跨系统)
1. 用户出示付款码
2. POS 机扫码
3. 用户核身
4. 商户确认并将现金交给用户
5. 交易完成

## 涉及服务/表
原文未提供。

## 校验点
- 用户核身：在商户交付现金前必须完成用户身份核验
