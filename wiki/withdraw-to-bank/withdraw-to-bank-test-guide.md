---
title: 提现功能测试方法
domain: withdraw-to-bank
kind: wiki_page
slug: withdraw-to-bank-test-guide
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:bc1e3b1d-5f33-4288-87a2-3ca7a3a28ca7
tags: []
---

# 提现功能测试方法

本页说明在测试环境下，使用 mock 渠道完成一笔提现到银行卡订单的全流程测试步骤，覆盖订单提交、结算与结果审核。相关业务背景见 [[withdraw-to-bank-overview]]。

## 测试前提

- 测试环境：渠道走 mock，不会真实出款到银行。
- 用户身份：根据测试目标准备 KYC 或 VIP 用户（页面字段差异见 [[withdraw-to-bank-page-rules]]）。
- 关注限额、费率与结算周期的取值，参见 [[withdraw-to-bank-limits-and-fees]]。

## 测试步骤

1. **APP 提交提现订单**
   - 在 APP 端进入 wallet-withdraw 或 home-Transfer 入口，按提现页规则填写 Account name、IBAN、Amount 等信息并提交。
   - 提交后账单与通知进入 Processing 状态（详见 [[withdraw-to-bank-bill-and-notification]]）。

2. **basis 查询并触发立即结算**
   - 在 basis 中根据用户/订单查询出对应的 payment order。
   - 通过"支付控制"功能对该订单执行立即结算。

3. **counter 管理置结果**
   - 在 counter 管理中找到对应订单，对订单状态进行置结果操作（成功 / 失败 / 退票等场景）。

4. **审核结果**
   - 进入"审核订单"中，对前一步置好的结果进行审核确认。
   - 审核通过后，订单状态正式落地。

## 验证点

- APP 端账单与通知文案是否随状态正确流转：Processing → Success / Transfer Failed / Declined by Your Bank。
- 结果页轮询行为：每 10 秒轮询一次，成功/失败终态后停止。
- 提现成功后是否自动将该卡绑定，并以提交时的 holder name 保存为 Bank_Account_Name。
- 失败场景下余额是否原路退回（无独立退款订单）。
- 退票场景下账单更新为 Declined by Your Bank，且不下发通知。

## 相关场景

完整端到端用例集合参见 [[scn_withdraw_to_bank_main_flows]]。
