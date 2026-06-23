---
title: ENBD/Liv 3DS认证页面说明
domain: acquire-transaction
kind: wiki_page
slug: enbd-3ds-authentication-screen
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:6a4051b7-2252-4757-a124-fe35cfe4bba0
tags: []
---

# ENBD/Liv 3DS认证页面说明

本页描述 Emirates NBD（Liv）作为发卡行在 Visa 卡交易中触发的 3-D Secure 步进式（step-up）认证页面，主要采用推送通知带外授权（out-of-band），并提供 SMS OTP 作为兜底方式。

## 页面品牌与标识

- 页脚品牌：`Powered by: Emirates NBD`（左）
- 卡组织标识：`VISA`（右）
- App 标识：推送通知顶部横幅显示 `liv` 应用图标

## 页面主标题与正文

- 主标题：`Authorize your transaction`
- 正文指引：提示用户在 `Liv X App` 上点击已发送的推送通知以完成授权
- 备选指引：用户也可以打开 `Liv X` App，进入 `Home` 区块完成授权

## 交易详情字段（Transaction details）

页面展示以下字段供用户核对：

- `Merchant`：商户名（示例：`PAYBY`）
- `Amount`：金额（示例：`Dhs. 1.00 AED`）
- `Card ending`：卡号尾号掩码（示例：`************3250`）
- `Date`：交易日期（示例：`20/10/2025`）

## 推送通知（主要认证方式）

iOS 推送横幅样式：

- 标题：`Card Payment Authorization`
- 时间戳：`now`
- 正文：`An online payment has been initiated with your card. Please review and verify the payment.`

主认证流程为带外推送：用户在 Liv X App 内审阅并确认交易即完成 3DS 授权。

## SMS OTP 兜底入口

- 区块标题：`Having trouble?`
- 兜底链接：`Try SMS OTP`

当用户无法通过推送/App 内审批时，可点击该链接切换到 SMS OTP 流程作为次级认证方式。

## 页脚与退出

- 帮助链接：`Need some help?`
- 认证说明链接：`Learn more about authentication`
- 退出链接：`Exit`（右对齐，点击中止认证）

## 认证方式总览

- 主认证：Liv X App 推送通知带外授权（或 App 内 Home 入口授权）
- 兜底认证：`Try SMS OTP`
- 终止操作：`Exit`
