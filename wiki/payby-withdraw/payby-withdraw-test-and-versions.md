---
title: 提现测试方法与版本迭代
domain: withdraw-cash
kind: wiki_page
slug: payby-withdraw-test-and-versions
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:tester/124289192
tags: []
---

# 提现测试方法与版本迭代

本页汇总 PayBy 提现到银行卡在测试环境下的 mock 渠道操作步骤，以及历史版本迭代记录，便于回归与历史追溯。相关业务规则见 [[payby-withdraw-overview]] 与 [[payby-withdraw-page-rules]]。

## 测试方法（mock 渠道）

测试环境通过 mock 渠道模拟银行返回结果，操作步骤：

1. APP 提交提现订单。
2. 通过 basis 查出对应的 payment order，再通过"支付控制"进行立即结算。
3. 在 counter 管理中对订单进行置结果操作。
4. 置结果后，进入"审核订单"对结果进行审核。

> 端到端流程参考 [[flow_payby_withdraw_to_bank]]，核心用例集见 [[scn_payby_withdraw_core_cases]]。

## 版本迭代记录

| 迭代版本 | 修改内容 |
| --- | --- |
| 2020/06/02 | totok (v1.3.8) 支持提现到银行卡功能 |
| 2020/06/10 | payby 安卓支持提现到银行卡功能 |
| 2020/07/11 | payby 安卓支持结果页面轮询 |
| 2020/08/07 | payby IOS 支持提现到银行卡功能，支持结果页面轮询，支持查询银行卡页面展示接口返回的 Bank_Account_Name |
| 2020/08/15 | payby 安卓：1) 支持查询银行卡页面展示接口返回的 Bank_Account_Name；2) History 改为 H5 账单 |
| 2020/09/27 | payby 安卓增加 home-transfer 入口，标题更名为 Transfer to Bank Account |
| 2020/09/30 | payby IOS 增加 home-transfer 入口，标题更名为 Transfer to Bank Account |

## 相关文档

- 产品原型：https://rv2lyl.axshare.com/#id=mxech9&p=%E6%9B%B4%E6%96%B0%E8%AE%B0%E5%BD%95&g=1
- 设计图：转账到银行卡-标注切图-0511.zip
