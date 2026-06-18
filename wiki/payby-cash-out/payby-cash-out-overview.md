---
title: PayBy Cash Out 业务总览
domain: payby-cash-out
kind: wiki_page
slug: payby-cash-out-overview
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:fe5f98bc-c2e2-43b6-862c-8e832eed6be0
tags: []
---

# PayBy Cash Out 业务总览

PayBy Cash Out 是一项让用户将 PayBy 钱包余额直接在 POS 端提现为现金（而非转入银行卡）的业务。

## 业务背景

- 面向有现金提取需求的 PayBy 用户。
- 提供一种区别于"提现到银行卡"的余额变现方式：余额 → 现金。
- 资金路径：用户 PayBy 余额 → 商户 POS → 现金交付用户。

## 交易流程概览

POS 现场办理 Cash Out 的关键步骤：

1. 用户在 PayBy 侧出示付款码。
2. 商户使用 POS 机扫描该付款码。
3. 用户完成核身。
4. 商户确认交易，并将相应金额的现金交付给用户。
5. 交易完成。

详细的端到端步骤见 [[flow_payby_cash_out_pos]]。
