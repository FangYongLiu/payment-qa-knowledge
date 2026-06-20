---
title: MoneyGram(MG)渠道说明
domain: fund-out-transfer
kind: wiki_page
slug: moneygram-channel-overview
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:5ee9e161-4776-4355-a881-8ba94d4d9171
tags: []
---

# MoneyGram(MG)渠道说明

本页记录 MoneyGram(MG)渠道在收款方扣费展示 UI 上的呈现内容，以及货币码拼写疑似异常的问题。

## 收款方费用展示 UI

在 MG 渠道的转账流程中，向发送方展示一个 "Receiver's Transfer Details" 卡片，用于告知 beneficiary 收款时将被扣除的费用。

- 标题：`Receiver's Transfer Details`
- 描述文案：`Your beneficiary will be charged the following fees once they receive the amount.`
- 费用条目（label 左对齐，金额右对齐，金额带负号表示扣减）：
  - `Receiver's Fee`：`-JYP 100.00`
  - `Tax Collection`：`-JYP 5.00`

## 货币码拼写问题（JYP / JPY）

UI 中费用金额前缀显示为 `JYP`，疑似为 `JPY`(日元)的拼写错误。

- 现状：两条费用行均使用 `JYP` 作为货币码
- 风险：`JYP` 并非标准 ISO 4217 货币码，可能为 typo
- 建议：QA 关注并核实是否应修正为 `JPY`
