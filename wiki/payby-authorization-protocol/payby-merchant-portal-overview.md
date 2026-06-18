---
title: PayBy商户控台(Merchant Portal)概览
domain: payby-authorization-protocol
kind: wiki_page
slug: payby-merchant-portal-overview
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:ea667653-6cbc-4ad0-9152-dbb1bbd83cdb
tags: []
---

# PayBy商户控台(Merchant Portal)概览

PayBy Merchant Portal 是 PayBy 商户/合作方使用的 Web 端控台，提供交易、账户、产品、门店、营销等核心运营功能的统一入口。

## 顶部信息栏

- 左侧：**PayBy MERCHANT** Logo
- 右侧：当前登录主体信息，例如 `AgentInformation0813(Merchant / Partner ID:200000428564)`
- 辅助图标：通知(铃铛)、帮助(?)、用户头像

## 左侧导航菜单

主导航(竖排)，默认选中 **Home**：

- **Home**
- **Transactions** → Fiat
- **Accounts** → Fiat
- **Statements**
- **Products** → Product List、Product Application、Paylink、Smart Code、Invoice、Transfer、Virtual Bank Account
- **ISV**(可折叠)
- **Offline Business** → Store、Device
- **Marketing**(可折叠)
- **Settings**

## 首页主区域

### Transactions Today(今日交易)

带 **History** 入口，展示当日核心指标：

- Transaction Amount(交易金额)，例：`AED 0.00`
- Transaction Count(交易笔数)
- Refund Amount(退款金额)，例：`AED 0.00`
- Refund Count(退款笔数)

### Current Balance(当前余额)

- 余额显示，例：`AED 99.63`
- 操作按钮：**Transfer**(深色)、**Deposit**(绿色)、**Withdraw**(橙色)
- 右上角 `...` 更多菜单

## Collect Money(收款方式)

四个卡片，前三个标注 **No code**(无需开发集成)：

- **Invoice** — Create an invoice：创建发票
- **Paylink** — Send a paylink：发送支付链接
- **Smart Code** — Create a smart code：创建智能码(二维码)
- **More ways to explore**：
  - Intelligent hardware — Apply(智能硬件申请)
  - API Management — Set(API 管理设置)
  - **More** 按钮，展开更多方式

## Other Accounts(其他账户)

- 占位卡片 **More Services Coming Soon**，更多服务即将上线
