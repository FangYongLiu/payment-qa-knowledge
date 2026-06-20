---
title: BASIS General Audit 审核记录页面说明
domain: risk-control
kind: wiki_page
slug: basis-general-audit-record-ui
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:d9e82a8a-bc4d-4d4e-8696-356ba4104819
tags: []
---

# BASIS General Audit 审核记录页面说明

本页介绍 PAYBY BASIS 后台 `General Audit > Audit Record` 页面的入口位置、筛选条件与列表字段，是风控核身规则等审核类操作的统一审核入口。

## 页面入口

- 系统：PAYBY BASIS（示例域名 `sim.intra.test2pay.com/basis/`）
- 左侧导航路径：`GENERAL > General Audit > Audit Record`
- 同级菜单：`Audit Log`
- 同属 GENERAL 分组的相关菜单：Union Query、Function Query、Log Monitor、Data Config、Open Auth、Query Config、User Resource、Business Monitor、Member Config、Mns Management、Cashier Auth、Protocol Config、Benefit、WPS、Product Mgt

## 筛选字段

页面顶部搜索栏支持以下条件，支持组合查询：

- `AuditId`：审核单号
- `AuditType`：审核类型（如 `GRC_IDENTITY_RULE`）
- `AuditStatus`：审核状态（如 `WAITING`）
- `ExecuteStatus`：执行状态
- `Fuzzy`：模糊匹配
- 日期区间：基于创建时间筛选（示例 `2025-03-17 00:00:00` ~ `2025-03-25 00:00:00`）
- `Search` 按钮触发查询

## 结果列表列说明

列表默认每页 10 条，分页展示。各列含义：

- `AuditId`：审核单唯一编号
- `AuditType`：审核类型枚举，例如 `GRC_IDENTITY_RULE`（风控核身规则相关变更）
- `Abbreviation`：操作摘要描述，例如 `Update Identity Rule`
- `Applier`：发起人账号
- `AuditStatus`：审核状态，例如 `WAITING`（待审核）
- `ExecuteStatus`：执行状态（审核通过后才有值）
- `CreateTime`：创建时间
- `UpdateTime`：更新时间
- `Action`：操作列，提供 `View`（查看）、`Audit`（审核）入口

## 风控核身规则审核入口

风控核身规则（业务域 risk-control）的变更通过本页面进行二次审核：

- 提交后会生成 `AuditType = GRC_IDENTITY_RULE`、`Abbreviation = Update Identity Rule` 的审核单
- 初始 `AuditStatus` 为 `WAITING`，由审核人在 `Action` 列点击 `Audit` 完成审批
- 审批通过后由系统执行变更，并回填 `ExecuteStatus`
