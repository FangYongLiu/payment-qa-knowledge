---
title: 提现到Aani流程
domain: withdraw-cash
kind: wiki_page
slug: withdraw-to-aani-flow
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:PCW/1972174889
tags: []
---

# 提现到Aani流程

本页描述用户通过 PayBy 客户端将钱包余额提现到 Aani 的端到端用户操作与界面交互过程。

## 流程概览

提现到 Aani 的用户侧流程主要包含以下界面阶段：

1. 发起提现（init）
2. 确认与身份校验（confirm & verify）
3. 提现成功（success）
4. 官方消息通知（official message）
5. 交易记录列表（transaction list）
6. 交易详情（transaction detail）

## 界面步骤

### Step 1：发起提现
用户在客户端进入提现到 Aani 入口，填写提现信息并发起请求（对应界面 `s1_init`）。

### Step 2：确认与身份校验
进入确认页，展示提现信息，用户完成身份校验（verify）后提交（对应界面 `s2_confirm_verify`）。

### Step 3：提现成功
身份校验与受理成功后，向用户展示提现成功结果页（对应界面 `s3_success`）。

## 通知与查询

- **官方消息（official message）**：提现处理结果会通过官方消息通知用户。
- **交易记录列表（transaction list）**：用户可在交易列表中查看本次 Aani 提现记录。
- **交易详情（transaction detail）**：进入单笔交易可查看本次提现的详细信息。

## 相关页面

- 同业务域的另一种提现渠道：[[withdraw-to-iban-flow]]
- 端到端时序与服务交互：[[flow_payby_withdraw_to_bank]]
