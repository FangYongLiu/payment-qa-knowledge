---
title: Counter System 余额监控界面
domain: payby-authorization-protocol
kind: wiki_page
slug: counter-system-balance-monitor-ui
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:ad6ea88d-e685-4a36-aeea-c286a1c459e7
tags: []
---

# Counter System 余额监控界面

Counter System 后台的 Balance Monitor 页面，用于查看与维护各渠道账户余额的同步监控配置。

## 页面入口

- 系统：Counter System（Welcome to Counter System）
- 面包屑：undefined / Balance Monitor

## 顶部工具栏

筛选输入项：

- Monitor
- Channel
- Account
- 下拉选项（默认值 YES）

操作按钮：

- Search
- Add
- Update Balance

## 数据表字段

表格列（从左至右）：

- Monitor N...（Monitor 名称）
- Channel C...（Channel Code）
- Bank Cod...（Bank Code）
- Account T...（Account Type）
- Account N...（Account No.）
- Balance
- Currency
- Monitor T...
- Sync Time
- Enable Fla...（Enable Flag）
- Sync Inter...（Sync Interval）
- Error Mes...（Error Message）
- Memo
- Create Ti...（Create Time）
- Update Ti...（Update Time）
- Action

## 示例数据

| Monitor | Channel | Bank | Account No. | Balance | Currency | Enable | Interval | Error |
|---|---|---|---|---|---|---|---|---|
| CKO201 | CKO201 | CKO | CKO201 | 44595.49 | AED | Y | 10 | queryAcc... |
| ENBD_Bal... | ENBD201 | ENBD | 33101109... | 1286672.41 | AED | Y | 30 | （空） |
| ENBD_204 | ENBD204 | ENBD | 10159103... | 3477.76 | AED | — | — | — |

- Account Type 列值示例：ACCOUN...
- Memo：CKO201 行有值，ENBD 行为空

## 行操作

- Action 列：Edit
