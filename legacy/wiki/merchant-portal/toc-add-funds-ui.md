---
title: ToC Add Funds 充值界面说明
domain: merchant-portal
kind: wiki_page
slug: toc-add-funds-ui
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:fea61db0-0761-468a-8220-cbc633c4a356
tags: []
---

# ToC Add Funds 充值界面说明

PayBy App 中 ToC 用户的 Add funds（充值）页面，由父页面与支付方式选择浮层组成，用于让用户确认金额并选择支付方式完成充值。

## 页面层级

- 父页面（Add funds）
  - 左上：返回箭头
  - 右上：`Deposit cash` 入口（蓝色链接）
  - 标题：`Add funds`
- 浮层（Bottom sheet 模态层）覆盖在父页面之上，父页面置灰

## 浮层内容结构

自上而下：

1. 右上角关闭按钮（X）
2. 插画：带紫色 "+" 硬币的钞票图
3. 金额展示：`AED 1.00`，下方副标题 `Add Funds`
4. 推广 CTA 行：`Link your bank account >`，右侧为银行/硬币插画，浅色渐变胶囊背景
5. 支付方式列表（卡片容器）
6. `Add payment method` 行（独立卡片，蓝色 "+" 图标 + 蓝色文字）
7. 底部主 CTA 按钮：`Pay →`（整宽，蓝色实心）

## 支付方式列表

列表项示例（含选中态与不可用态）：

1. **Apple Pay** — Apple Pay logo，未选中
2. **Debit Card (3250)** — Visa logo，已选中（蓝色实心 radio）
3. **Debit Card (6789)** — Mastercard logo，未选中
4. **Credit Card (4683)** — Visa logo，置灰，副标题 `Unavailable for this service`，radio 禁用

说明：
- 选中态使用蓝色实心 radio
- 不可用方式仍展示在列表中，但 radio 禁用且附原因文案

## 主流程与备选路径

主流程：
- 用户进入 Add funds → 确认金额（如 `AED 1.00`）→ 选择一个可用支付方式（示例为 Visa Debit 尾号 3250）→ 点击 `Pay` 提交充值

备选路径：
- 点击 `Link your bank account` 去绑定银行账户
- 点击 `Add payment method` 新增支付方式
- 点击父页面右上角 `Deposit cash` 走现金存入流程
