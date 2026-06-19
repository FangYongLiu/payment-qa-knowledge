---
title: PayBy 发布流程
domain: merchant-acquisition-testing
kind: wiki_page
slug: payby-release-process
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:9af06167-7905-4fb3-8d8c-f2f6c96e5abd
tags: []
---

# PayBy 发布流程

PayBy 发布流程跨 DEV、SIM、UAT、PROD 四个环境，由 DEV、QA、Devops/DBA 三类角色协作完成，从开发自测一路推进到生产验证并产出测试报告。

## 角色与环境

- **环境**：DEV → SIM → UAT → PROD
- **角色**：
  - DEV：开发与自测、提交 PR、合并 Master
  - QA：SIM 测试、UAT 测试、回归测试、生产验证
  - Devops/DBA：DB 变更、部署、发布

## DEV 阶段

- Development（开发）：未 Done 则继续开发
- Self Test（自测）：未 Done 则回到开发，Done 后进入 SIM

## SIM 阶段

- DEV：Submit PR → Merge to Master → 确认 Done
- QA：Wait Test → SIM Test → 判定 Passed
  - 未通过：Reopened，回退到 DEV 的 Development 重新开发
  - 通过：进入 UAT

## UAT 阶段

- QA 判定 **All**：
  - **CR** 分支：循环处理
  - **DB Change** 分支：由 Devops/DBA 执行 **UAT DB CHANGE**
  - 无 DB 变更：直接进入部署
- Devops/DBA：UAT DEPLOY → 判定 DONE
- QA：UAT Test → 判定 Passed
  - 未通过：回到 UAT DEPLOY
- 通过后判定 **All?** → Regression Test（回归测试） → 判定 Passed
  - 未通过：回到 UAT DEPLOY
  - 通过：进入 PROD

## PROD 阶段

- Devops/DBA：PROD DB CHANGE → PROD DEPLOY → 判定 DONE
- QA：PROD Validation（生产验证） → 判定 Passed
  - 未通过：回到 PROD Validation 或 PROD DEPLOY
- 通过后输出 **Release Test Report**（发布测试报告，流程终点）

## 关键流转规则

- SIM 测试不通过会触发 Reopened，回到开发起点
- UAT 阶段的 DB 变更必须先于部署执行
- UAT 测试与回归测试任一不通过，均回退到 UAT DEPLOY 重新部署验证
- 生产验证失败可回退至 PROD Validation 或 PROD DEPLOY
- 全流程以 Release Test Report 作为发布闭环标志
