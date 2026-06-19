---
title: 人工资金调拨操作指南
domain: authorization-protocol
kind: wiki_page
slug: manual-fund-transfer-counter-system
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:078c7129-4240-46dc-b176-a5c4ee25fede
tags: []
---

# 人工资金调拨操作指南

本页说明在 Counter System 后台执行人工资金调拨（Apply Settlement）的入口位置与结算明细列表字段。

## 操作入口

- 系统：**Counter System** 后台
- 页面路径：`Settlement Detail`（结算明细）
- 操作按钮：页面顶部工具栏右侧的蓝色 **Apply Settlement** 按钮，点击发起人工资金调拨

## 顶部筛选/工具栏

- 业务类型下拉（示例值：`CA向CA内部`）
- `Status` 状态下拉
- 时间范围选择器，格式：`YYYY-MM-DD HH:mm:ss - YYYY-MM-DD HH:mm:ss`
- `Search` 查询按钮（绿色）
- `Apply Settlement` 发起结算按钮（蓝色）

## 结算明细表字段

列表展示已发起/已处理的结算单，主要列如下：

- **Business Type**：业务类型（如 `CA向CA内部`）
- **Settlement No**：结算单号
- **Settlement Date**：结算日期
- **Settlement Type**：结算类型（示例：`MANUAL` 人工）
- **Voucher**：凭证号
- **Settlement Amount**：结算金额
- **Settlement Currency**：结算币种（示例：`AED`）
- **Target Account / Target ...**：目标账户相关信息
- **Fee Amount**：手续费金额
- **File Url**：附件/文件链接
- **Operator**：操作人
- **Audit Status**：审核状态（示例：`PASS`）
- **Settlement Result**：结算结果（示例：`SUCCESS` / `FAIL`）
- **Result Code / Msg**：结算结果码与描述（失败示例：`FTD-06...`）
- **Memo**：备注
- **Create Time** / **Update Time**：创建时间 / 更新时间
- **Action**：操作列（示例操作：`Update Status` 更新状态）

## 示例数据参考

- `20250120`，`MANUAL`，金额 `77 AED`，Audit `PASS`，Settlement `SUCCESS`
- `MANUAL`，金额 `66 AED`，Audit `PASS`，Settlement `FAIL`，Result `FTD-06...`
- `20250117`，`MANUAL`，金额 `300 AED`，Audit `P...`

> 说明：`MANUAL` 类型记录均通过 **Apply Settlement** 入口由操作人发起；失败记录可在 `Action` 列通过 `Update Status` 维护状态。
