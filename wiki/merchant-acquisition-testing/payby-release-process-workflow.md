---
title: PayBy发布流程状态流转
domain: merchant-acquisition-testing
kind: wiki_page
slug: payby-release-process-workflow
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:d03911bf-4a54-4dca-ad76-e499b938cb4f
tags: []
---

# PayBy发布流程状态流转

本页描述 PayBy Release Process 中 Jira 任务的状态机流转，覆盖从 `NEW TASK` 到 `COMPLETED` / `SECURITY COMPLETED` 的完整路径。

## 状态节点

工作流包含以下状态节点：

- `NEW TASK`（起始状态）
- `IN DEVELOPING`
- `WAIT TEST`（等待/中间态）
- `SIM TESTING`
- `UAT DB CHANGE`
- `UAT DEPLOY`
- `UAT TESTING`
- `SECURITY CONFIRM`
- `TECH LEAD CONFIRM`
- `QA LEAD CONFIRM`
- `PROD DB CHANGE`
- `PROD DEPLOY`
- `PROD VERIFY`
- `COMPLETED`（终态）
- `SECURITY COMPLETED`（终态）
- `MANAGER CONFIRM`（游离节点，未连入主流程）

## 主流程流转（UAT 阶段）

从 `NEW TASK` 起，依次顺序流转：

1. `NEW TASK` → `IN DEVELOPING`
2. `IN DEVELOPING` → `WAIT TEST`
3. `WAIT TEST` → `SIM TESTING`
4. `SIM TESTING` → `UAT DB CHANGE`
5. `UAT DB CHANGE` → `UAT DEPLOY`
6. `UAT DEPLOY` → `UAT TESTING`

`UAT TESTING` 完成后，流程切换到确认与生产部署阶段。

## 主流程流转（确认与生产阶段）

从 `UAT TESTING` 进入：

1. `UAT TESTING` → `SECURITY CONFIRM`
2. `SECURITY CONFIRM` → `TECH LEAD CONFIRM`
3. `TECH LEAD CONFIRM` → `QA LEAD CONFIRM`
4. `QA LEAD CONFIRM` → `PROD DB CHANGE`
5. `PROD DB CHANGE` → `PROD DEPLOY`
6. `PROD DEPLOY` → `PROD VERIFY`
7. `PROD VERIFY` → `COMPLETED`
8. `COMPLETED` → `SECURITY COMPLETED`

## 特殊路径

- **跳转路径**：`QA LEAD CONFIRM` 可直接跳转到 `PROD VERIFY`，跳过 `PROD DB CHANGE` 与 `PROD DEPLOY`。
- **回退路径**：标记为 `All` 的转移指向 `NEW TASK`，表示任意状态均可回退到 `NEW TASK`。
- **游离节点**：`MANAGER CONFIRM` 未与主流程连线。

## 终态标识

- `COMPLETED`：常规发布终态。
- `SECURITY COMPLETED`：在 `COMPLETED` 之后经安全确认到达的最终态。

相关：[[payby-release-process-workflow]]
