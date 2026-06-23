---
title: Paylink支付链接
domain: merchant-portal
kind: wiki_page
slug: merchant-portal-paylink
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_attachment
source_ref: wiki_attachment:0e957eb2-a24a-4257-b773-ebccfac51613
tags: []
---

# Paylink支付链接

Paylink 把一条收款链接/嵌入代码交给商户，可以放到社媒或网页按钮上，顾客点开即可完成支付。

## 业务流程

1. 商户在控台创建 Paylink。
2. 商户把 Paylink 发送给顾客，或将按钮代码嵌入到自己的网页 / 社交媒体。
3. 顾客打开链接（或点击按钮）完成支付。
4. 支付成功后，商户会收到一封支付成功邮件通知。

## 创建入口

- 路径：[Products] – [Paylink] – [ADD NEW]
- 创建前需先完成 [[merchant-portal-product-application]]，开通 Paylink 产品。

## 设置 Paylink

创建页面可配置以下内容：

- **Paylink description**：填写该 Paylink 的描述。
- **按钮样式**：勾选对应选项后可编辑按钮样式。
- **商品信息**：勾选后可添加商品（product details），并可设置顾客是否可以修改商品数量（quantity）。
- **Logo**：可选，支持上传 logo。

## 获取代码 / 链接

Paylink 创建完成后，可在列表中：

- 编辑（Edit）已创建的 Paylink。
- 复制 **code**：用于嵌入网页（按钮形式）。
- 复制 **link**：直接发送给顾客或贴到社媒。

## 顾客支付与商户通知

- 顾客点击 Paylink 进入支付页并付款。
- 支付完成后，商户会收到一封通知邮件。
- 如需对该笔订单进行退款，参考 [[merchant-portal-refund]]；款项结算与提现见 [[merchant-portal-settlement-and-withdraw]]。

## 相关收款方式

- 线下扫码收款：[[merchant-portal-smart-code]]
- 发票收款：[[merchant-portal-invoice]]
