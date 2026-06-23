---
title: 提现到银行卡功能总览
domain: withdraw-cash
kind: wiki_page
slug: withdraw-to-bank-overview
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:bc1e3b1d-5f33-4288-87a2-3ca7a3a28ca7
tags: []
---

# 提现到银行卡功能总览

Transfer to Bank Account（Transfer to your Bank）是用户将 PayBy 余额账户资金转出至银行卡账户的功能，资金最终离开 PayBy 体系流向银行。

## 业务描述

- 业务双方为用户与银行，区别于一般的用户间交易。
- 资金流向：用户余额账户 → 银行卡账户。
- 功能英文名：Transfer to Bank Account / Transfer to your Bank。

## 常用场景

1. 用户进入提现页面，输入信息并提交提现，收到通知与账单。
2. 银行返回成功，用户收到通知，账单更新。
3. 银行返回失败，用户收到通知，账单更新，资金原路退回（无退款订单）。
4. 银行成功后发生退票，用户无通知，账单状态更新。

## 功能入口

- wallet → withdraw → Transfer to Bank Account
- home → Transfer → Transfer to Bank Account
- 平台覆盖：iOS、Android。

## 主要页面与子模块

完整页面交互与字段校验规则参见 [[withdraw-to-bank-page-rules]]：

- 提现页面（输入 Account name / IBAN / Bank name / Amount，校验与录入规则）。
- Select Bank Account 页面（已绑定提现卡列表、左滑删除、提现成功后自动绑卡）。
- History 页面及结果页轮询（注：Android History 已改为对接 H5 账单，现已无此内容）。

相关延伸：

- 账单与通知状态对应关系见 [[withdraw-to-bank-bill-and-notification]]。
- 限额、费率、结算周期及收银台与风控规则见 [[withdraw-to-bank-limits-and-fees]]。
- 测试方法（mock 渠道、basis、counter 审核流程）见 [[withdraw-to-bank-test-guide]]。
- 主流程场景集见 [[scn_withdraw_to_bank_main_flows]]。

## 版本迭代

| 时间 | 修改内容 |
| --- | --- |
| 2020/06/02 | totok（v1.3.8）支持提现到银行卡功能 |
| 2020/06/10 | PayBy Android 支持提现到银行卡功能 |
| 2020/07/11 | PayBy Android 支持结果页面轮询 |
| 2020/08/07 | PayBy iOS 支持提现到银行卡功能，支持结果页面轮询，支持查询银行卡页面展示接口返回的 Bank_Account_Name |
| 2020/08/15 | PayBy Android：1) 支持查询银行卡页面展示接口返回的 Bank_Account_Name；2) History 改为 H5 账单 |
| 2020/09/27 | PayBy Android 增加 home-transfer 入口，标题更名为 Transfer to Bank Account |
| 2020/09/30 | PayBy iOS 增加 home-transfer 入口，标题更名为 Transfer to Bank Account |

## 相关文档

- 产品原型：https://rv2lyl.axshare.com/#id=mxech9&p=%E6%9B%B4%E6%96%B0%E8%AE%B0%E5%BD%95&g=1
- 设计图：转账到银行卡-标注切图-0511.zip
