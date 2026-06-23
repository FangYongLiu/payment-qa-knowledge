---
title: Basis 风控核身规则管理后台
domain: risk-control
kind: wiki_page
slug: basis-identity-rule-management
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:ab1619cc-aafa-4cd5-9432-b7e096048d75
tags: []
---

# Basis 风控核身规则管理后台

介绍 PAYBY BASIS 后台中风控核身规则（Identity Rule）的管理页面入口、筛选字段、规则列表字段及新增规则入口。

## 页面入口

导航路径：`RISK CONTROL` > `Risk Event` > `Identity Rule Management`。

`Risk Event` 下的同级子菜单包括：

- Server Switch Management
- Engine Score Management
- Status Score Management
- Merge Score Record
- Identity Decision
- **Identity Rule Management**（本页）
- Identity Variables

## 筛选与操作栏

页面顶部筛选/操作控件：

- EventType 下拉（如 `PAYMENT`）
- ID 输入框
- Rules 输入框
- Status 下拉（如 `Active`）
- 按钮：`Search`、`Reset`、`Add`

点击 `Add` 用于"新增 1 条风控规则"。

## 规则列表字段

规则表格包含以下列：

- EventType
- Rules
- IdentityType
- Priority
- RelatedId
- Status
- IsRejected
- ignoreRe...（ignore 相关字段）
- Remarks
- CreateTime
- CreateBy
- UpdateTime
- UpdateBy
- Action

## 示例规则

一条 `PAYMENT` 事件下的核身规则示例：

- EventType：`PAYMENT`
- Rules：`memberId==100000431355`
- IdentityType：`THREEDS`
- Priority：`-3`
- IsRejected：`NO`
- ignore：`NO`
- Remarks：`2`
- Status：`Active`
- CreateTime：`2025-01-08 16:11:25`
- CreateBy：`feng`
