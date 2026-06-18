---
title: Merchant Portal(BMOC商户控台)概览
domain: payby-authorization-protocol
kind: wiki_page
slug: merchant-portal-bmoc-overview
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:43417768-3cf2-4181-b239-d39e16058007
tags: []
---

# Merchant Portal(BMOC商户控台)概览

BMOC 商户控台是 PayBy 的后台管理 UI，提供商户基础信息维护、产品开通管理与审核等功能入口。

## 访问入口

- 环境地址（UAT）：`uat-admin.corp.test2pay.com/bmoc/`
- 顶部工具栏：折叠、刷新、Home、语言切换（English）、通知（带未读徽标）、全屏、用户头像
- 标签页（Tab）支持多页签并存与关闭，如 `Home`、`Mercht Open Product`、`Apply Audit`

## 左侧导航结构

顶层应用名 `BMOC`，主要分组如下：

- **Basis**
- **Basis Merchant**
- **GENERAL**
  - **Product Mgt**
    - **ProductOpenMgt**
      - `Mercht Open Product`
      - `Batch Open Product`
      - `ProdRate & Settle...`（产品费率与结算相关）
    - **Product Audit**
      - `Apply Audit`
      - `Config Audit`

## Mercht Open Product（商户已开通产品查询）

`ProductOpenMgt` 下的入口，用于按商户查询其已开通的产品列表。

查询表单字段：

| 字段 | 必填 | 说明 |
|---|---|---|
| MerchantId | 是（红色 `*`） | 输入框 placeholder：`Please input merchantId` |

操作按钮：

- `Inquire`：根据输入的 MerchantId 发起查询
- `Reset`：清空表单

初始状态下表单为空，未展示结果列表，需输入 MerchantId 后查询。
