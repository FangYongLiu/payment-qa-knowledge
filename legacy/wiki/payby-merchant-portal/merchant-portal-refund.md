---
title: 退款操作与授权
domain: merchant-portal
kind: wiki_page
slug: merchant-portal-refund
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_attachment
source_ref: wiki_attachment:0e957eb2-a24a-4257-b773-ebccfac51613
tags: []
---

# 退款操作与授权

商户在 PayBy Merchant Portal 中可针对已完成的法币订单发起退款，退款需要经过管理员或财务账号的授权后方可生效。

## 发起退款

- 入口：[Transaction] – [Fiat]
- 在交易列表中找到目标订单，点击 [Refund]
- 由发起人提交退款请求

## 授权规则

- 退款必须经过授权才能完成
- 可授权账号：admin 账号 / financial 账号
- 若由 financial staff 发起：需由 admin 或 另一个 financial 账号 进行授权

## 授权操作

- 授权人（admin / financial 账号）登录后进入：[Settings] – [Authorizations]
- 在列表中找到对应订单
- 点击 [Refund] 完成授权

## 相关页面

- 提现也遵循相同的双人授权机制，详见 [[merchant-portal-settlement-and-withdraw]]
- 员工账号的添加与权限设置见 [[merchant-portal-account-management]]
- 查看订单与对账单见 [[merchant-portal-statements]]
