---
title: ENBD Channel - Balance Monitor界面说明
domain: payby-authorization-protocol
kind: wiki_page
slug: enbd-channel-balance-monitor-ui
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:c24e6fff-2d6b-4b3a-a5f8-a398a127c19b
tags: []
---

# ENBD Channel - Balance Monitor界面说明

本页描述 Counter System 后台中 `Account` 菜单下 `Balance Monitor` 页面的 UI 布局、筛选项与数据表字段。

## 页面入口

- 系统：Counter System
- 左侧菜单路径：`Account` → `Balance Monitor`
- 同级子菜单还包括：`Account Info`、`Account Management`、`Accounting Transfer...`、`Accrual`、`Run up an Account`、`OnAccount`、`VvipMonitor`、`Balance Monitor`、`CBFileSummary`

## 顶部通用栏

- 折叠菜单按钮、刷新按钮
- 欢迎语：`Welcome to Counter System`
- `Language` 语言切换下拉
- 通知铃铛、全屏按钮、用户头像（示例用户：周晓妍）
- 面包屑：`undefined / Balance Monit...`

## 筛选与操作区

筛选输入控件（共 4 个）：

- `Monitor`（文本输入）
- `Channel`（文本输入）
- `Account`（文本输入）
- 启用状态下拉，默认值 `YES`

操作按钮：

- `Search`（搜索）
- `Add`（新增）
- `Update Balance`（刷新余额）

## 数据表字段

列顺序（部分列名因表格宽度被截断，以下为显示文案）：

1. `Monitor ...`
2. `Channel...`
3. `Bank C...`（Bank Code）
4. `Account...`
5. `Account...`
6. `Balance`
7. `Currenc...`（Currency）
8. `Monitor ...`
9. `Sync Ti...`（Sync Time）
10. `Enable ...`
11. `Sync Int...`（Sync Interval）
12. `Error M...`（Error Message）
13. `Memo`
14. `Create ...`
15. `Update ...`
16. `Action`

## 示例数据

表格示例行（共 1 条有效数据示意）：

| 字段 | 值 |
|---|---|
| Monitor | CKO201 |
| Channel | CKO201 |
| Bank Code | CKO |
| Account | ACCOU... |
| Account | CKO201 |
| Balance | 4896503 |
| Currency | AED |
| Monitor | 10 |
| Sync Time | 2025-03... |
| Enable | Y |
| Sync Interval | (blank) |
| Error Message | (blank) |
| Memo | CKO201 |
| Create | 2025-03... |
| Update | 2025-03... |
| Action | Ed（Edit） |
