---
title: PayBy Merchant Portal(商户控台)概览
domain: payby-authorization-protocol
kind: wiki_page
slug: payby-merchant-portal-overview
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:803dfa07-8424-4b13-8da1-2740e7945bbd
tags: []
---

# PayBy Merchant Portal(商户控台)概览

PayBy Merchant Portal 是 PayBy 提供给商户的 Web 端管理控台，支持交易查询、账户管理、对账单下载、产品配置、线下业务与营销等运营操作。

## 导航结构

左侧主导航包含以下菜单项：

- **Home**
- **Transactions**（可展开） → Fiat
- **Accounts**（可展开） → Fiat
- **Statements**（对账单）
- **Products**（可展开） → Product List、Product Application、Paylink、Smart Code、Invoice、Transfer、Virtual Bank Account、Digital Receipt
- **Offline Business**（可展开）
- **Marketing**（可展开）
- **Settings**

## Statements 对账单页面

Statements 页面用于按周期查看与下载商户的对账数据。

### 顶部操作

- 页面标题：**Statements**
- **Subscribe**（订阅）按钮：以铃铛图标形式置于标题旁，用于订阅对账单。

### Tab 分类

- 一级 Tab：**Transaction**（交易）/ **Settlement**（结算）
- 二级 Tab：**Daily**（按日）/ **Monthly**（按月）

### 过滤条件

- 日期范围筛选（Date Range），例如 `22-01-2025 ~ 22-02-2025`。

### 数据表格字段

| 列名 | 说明 |
|---|---|
| Date | 对账单所属日期 |
| Start Time | 统计起始时间 |
| End Time | 统计结束时间 |
| Records Count | 记录条数 |
| Download | 下载入口（图标） |

示例：`21-02-2025` 这一行的 Start Time 为 `21-02-2025 00:00:00`，End Time 为 `22-02-2025 00:00:00`，Records Count 为 `11`，即按自然日（00:00:00 ~ 次日 00:00:00）切片汇总当日交易记录数，并提供单日下载入口。
