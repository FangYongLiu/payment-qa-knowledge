---
title: PayBy 发布流程
domain: merchant-acquisition-testing
kind: wiki_page
slug: payby-release-process
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:7d0ce586-3ad3-48b8-a702-c1e6738e28a1
tags: []
---

# PayBy 发布流程

PayBy 发布流程跨 DEV、SIM、UAT、PROD 四个环境，由 DEV、QA、Devops/DBA 三个角色协作完成，从开发自测一路推进到生产发布。

## 角色与环境

- **角色（泳道）**：DEV、QA、Devops/DBA
- **环境（阶段）**：DEV、SIM、UAT、PROD

## DEV 阶段（开发自测）

由 DEV 负责：

1. **Development**：开发完成后判断 Done，未完成则回到 Development。
2. **Self Test**（自测）：完成后判断 Done，未通过回到自测。

## SIM 阶段（SIM 测试）

由 DEV 提交、QA 验证：

1. 流转到 QA 的 **Wait Test** → **SIM Test**。
2. 判断 **Passed**：
   - 若被 **Reopened**（虚线回退），回到 DEV 的 Development。
   - 若通过，DEV 执行 **Submit PR** → **Merge to Master** → 判断 Done。

## UAT 阶段（UAT 部署与回归）

由 QA 决策、Devops/DBA 执行部署：

1. QA 判断 **All**：
   - **CR** 分支：循环回退。
   - **DB Change** 分支：先由 Devops/DBA 执行 **UAT DB CHANGE**（虚线），再进入 **UAT DEPLOY**。
   - 其他情况：直接进入 **UAT DEPLOY**。
2. **UAT DEPLOY** → 判断 DONE → QA 执行 **UAT Test** → 判断 **Passed**：
   - 未通过：回到 **UAT DEPLOY**。
   - 通过：判断 **All?** → **Regression Test** → 判断 **Passed**：
     - 未通过：回到 **UAT DEPLOY**。

## PROD 阶段（生产发布）

由 Devops/DBA 负责 PROD 部署（PROD D…）。

## 关键决策与回环

- **Done**（Development / Self Test / Merge to Master / UAT DEPLOY）：未完成均回到当前节点。
- **Passed**（SIM Test / UAT Test / Regression Test）：未通过分别回到 Development 或 UAT DEPLOY。
- **Reopened**：SIM 测试后将问题打回到 DEV 开发。
- **All / All?**：用于判断是否覆盖全部范围（含 CR、DB Change 分支判定与回归触发）。

相关：[[payby-release-process]]
