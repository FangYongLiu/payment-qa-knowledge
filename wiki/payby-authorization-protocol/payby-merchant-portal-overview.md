---
title: PayBy商户控台(Merchant Portal)概览
domain: payby-authorization-protocol
kind: wiki_page
slug: payby-merchant-portal-overview
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:839d04fa-65dc-4d8b-81ce-a40b71781159
tags: []
---

# PayBy商户控台(Merchant Portal)概览

PayBy Merchant Portal 是商户侧的 Web 管理控台，提供交易、账户、对账单、商品、线下业务、营销与设置等模块入口。

## 左侧导航结构

控台左侧主导航（自上而下）：

- Home
- Transactions
  - Fiat
- Accounts
  - Fiat
- Statements
- Products
- Offline Business
  - Store
  - Device
- Marketing
- Settings

## Offline Business / Store 页面

`Offline Business → Store` 进入 **Store Management**（门店管理）页面，用于查看商户已注册的线下门店列表。

列表字段：

| 列 | 含义 |
| --- | --- |
| Store ID | 门店唯一编号 |
| Store Name | 门店名称 |
| Address Line1 | 地址第一行 |

示例数据：

- 28661 / Sim Store Register02 / Sky Tower
- 28660 / Sim Store Register01 / Sky Tower
- 28611 / phoneNumberTest / Sky Tower
- 28603 / BASIS_Store / Sky Tower
- 28602 / EDISON LED LIGHTING / EDISON LED LIGHTING
- 28601 / SIM Edison01 / Sky Tower

## 同级子菜单

`Offline Business` 下除 Store 外还包含 **Device**（设备管理），用于线下设备相关配置。
