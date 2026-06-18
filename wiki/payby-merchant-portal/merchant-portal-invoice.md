---
title: Invoice开票收款
domain: payby-merchant-portal
kind: wiki_page
slug: merchant-portal-invoice
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_attachment
source_ref: wiki_attachment:0e957eb2-a24a-4257-b773-ebccfac51613
tags: []
---

# Invoice开票收款

通过 Invoice 功能向客户的手机或邮箱发送账单，客户点击即可在线支付，支付成功后商户会收到邮件通知。

## 业务流程

1. 商户在控台创建 Invoice
2. 将 Invoice 发送至客户的手机号 / 邮箱
3. 客户接收并完成支付
4. 商户收到支付成功邮件

## 创建入口

进入 [Products] – [Invoice] – [CREATE INVOICE]。

## 填写发票信息

在创建页面填写以下内容：

- **Customer name**：客户姓名
- **Products information**：商品/服务明细
- **Due date**：到期日
- **客户联系方式**：手机号或邮箱（用于接收 Invoice）
- **VAT**：选择税率；填写 TRN 后可选择 5%
- **Discount**：折扣金额或百分比
- **Title**：可选 Invoice / Bill / Tax Invoice
- **Overdue rule**：到期未付时保留(keep) 或取消(cancel)

## 操作选项

填写完成后可执行：

- **PREVIEW**：预览 Invoice
- **SEND**：保存并直接发送给客户
- **SAVE AS INVOICE**：保存为已定稿 Invoice，保存后不可再编辑，可后续 SEND 给客户
- **SAVE AS DRAFT**：保存为草稿，后续可编辑

## 支付与通知

- 客户在收到的 Invoice 中点击链接完成支付
- 支付成功后，商户会收到邮件通知

## 相关功能

- 若需开具正式税务发票，参见 [[merchant-portal-tax-invoice]]
- 用于线上链接收款可参考 [[merchant-portal-paylink]]
- 用于线下扫码收款可参考 [[merchant-portal-smart-code]]
- 收款后的退款流程参见 [[merchant-portal-refund]]
