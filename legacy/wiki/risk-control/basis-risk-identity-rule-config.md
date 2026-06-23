---
title: Basis 风控核身规则配置说明
domain: risk-control
kind: wiki_page
slug: basis-risk-identity-rule-config
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:6aecff26-c4e6-42bb-886d-ffbfd96cf983
tags: []
---

# Basis 风控核身规则配置说明

本页说明 Basis 后台“核身规则管理”（Identity Rule Management）页面的入口位置、列表字段与新增规则操作入口。

## 页面入口

在 Basis 后台左侧导航中：

- 一级菜单：`RISK CONTROL`
- 二级分组：`Risk Event`
- 进入页面：`Identity Rule Man...`（Identity Rule Management）

同分组下还可见相关菜单：`Risk Audit`、`WPS Project`、`Server Switch Ma...`、`Engine Score Man...`、`Status Score Man...`、`Merge Score Record`、`Identity Decision...`、`Identity Variables...`、`Risk Inquiry`。

## 规则列表字段

列表展示已配置的核身规则，主要列包括：

- `ID`
- `EventType`：事件类型，例如 `AAE_ADD_BENEFI...`、`AAE_DOWNLOAD_...`、`AAE_OPEN`、`ACCOUNT_CANCEL`、`AUTO_DEBIT_PAY...` 等
- `Rules`：规则表达式片段，例如 `riskScore<=1000`、`isNeedIdentifyHint=='Y'`、`isNeedIdentifyHint=='N'`、`hadP...` 等
- `Remarks`：备注
- `CreateTime` / `CreateBy`
- `UpdateTime`

行附加属性还包括状态 `Active`、`IsRejected`（如 `NO`）以及优先级 `priority`（如 `1`、`2`）。列表支持分页浏览。

## 新增核身规则

页面提供 `Add Identity Rule` 弹窗用于新增规则，在该弹窗中按事件类型与规则表达式录入并保存即可生效到列表中。
