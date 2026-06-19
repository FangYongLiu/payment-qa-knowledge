---
title: 提现到Aani流程
domain: withdraw-cash
kind: wiki_page
slug: withdraw-to-aani-flow
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:4efb14db-9f70-47c4-98d9-b2969c863ce6
tags: []
---

# 提现到Aani流程

本页概述用户通过 Aani 渠道发起提现的端到端业务流程概览。相关渠道差异参见 [[withdraw-to-iban-flow]]，底层技术调用链参见 [[flow_payby_withdraw_to_bank]]。

## 业务范围

- 业务域：`withdraw-cash`
- 渠道：Aani
- 覆盖：用户从发起提现到资金落地的完整用户侧操作与交易流程

## 用户操作流程

按照原文截图顺序，用户侧主要经历以下步骤：

1. **发起提现**（`s1_init`）：用户在提现入口选择 Aani 渠道并填写提现信息。
2. **确认与身份校验**（`s2_confirm_verify`）：确认提现信息并完成身份验证。
3. **提现成功**（`s3_success`）：展示提现成功结果页。

## 通知与查询

- **官方消息通知**（`official_message`）：提现完成后向用户发送官方消息提醒。
- **交易列表**（`transaction_list`）：用户可在交易列表中查看 Aani 提现记录。
- **交易详情**（`transaction_detail`）：进入单笔记录可查看该笔 Aani 提现的详情信息。

## 相关流程

- IBAN 渠道的提现流程：[[withdraw-to-iban-flow]]
- 提现到银行卡的端到端技术流程（下单、支付、批处理）：[[flow_payby_withdraw_to_bank]]
