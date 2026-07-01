---
id: flow_payby_cash_in
object_type: Flow
name: 现金充值流程 (Cash In via POS)
aliases: [Cash In, 现金充值]
domain: wallet
status: active
owner: qianlong.wang
reviewer: qianlong.wang
last_reviewed_at: '2026-06-24'
source_type: wiki
source_ref: 'wiki:3c10a914-4e15-4684-a1b5-a24d41fb7577'
tags: [wallet, cashin, pos, 现金充值, deposit]
related_services: []
related_tables: []
related_scenarios: []
---

# 现金充值流程 (Cash In via POS)

## 概述
Cash In 是 PayBy 的现金充值业务:用户将现金交付线下商户,商户通过 POS 系统将等额资金充入用户 PayBy 余额账户。与"现金提现 Cash Out"([[flow_payby_cash_out]])方向相反——Cash In 是现金→余额,Cash Out 是余额→现金。面向有现金充值需求的用户。

## 步骤(跨系统)
1. 用户出示**静态码**(承载会员信息,作为充值账户标识)。
2. 商户用 **POS 机**扫描该静态码。
3. 商户在 POS 机上输入充值金额。
4. 用户确认交易。
5. 用户将等额现金交付商户。
6. 交易完成,资金充入用户 PayBy 余额。

## 关联关系
- **经过的服务(有序)**:待补(原文未给系统侧调用链与服务列表)。
- **关键表**:待补。
- **相关流程**:反方向的现金提现见 [[flow_payby_cash_out]]。

## 校验点
- 静态码有效性与会员信息识别(POS 扫码)。
- 充值金额录入与用户确认。
- 资金充入用户余额的落库/到账:待补(原文未给落库表与对账点)。
