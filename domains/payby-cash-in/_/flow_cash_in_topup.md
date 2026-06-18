---
id: flow_cash_in_topup
object_type: Flow
domain: payby-cash-in
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: confluence:tester/124289139
tags: []
subdomain: null
module: null
sensitivity: normal
name: Cash In 现金充值流程
aliases: []
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 概述
用户有现金充值需求，将现金充入 payby 余额。流程通过用户出示静态码（含会员信息），由商户 POS 机扫码并输入金额，用户确认后将现金交给商户，完成余额充值交易。

## 步骤(跨系统)
1. 用户出示静态码（含会员信息）
2. POS 机扫描静态码
3. POS 端输入充值金额
4. 用户确认交易
5. 用户将现金交给商户
6. 完成交易，金额充入 payby 余额

## 涉及服务/表
原文未明确说明。

## 校验点
- 静态码须包含会员信息
- 用户确认环节
- 现金交付与交易完成的对应关系

</details>
