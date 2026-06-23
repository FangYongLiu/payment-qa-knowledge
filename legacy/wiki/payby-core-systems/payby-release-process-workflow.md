---
title: PayBy发布流程状态流转
domain: payby-core-systems
kind: wiki_page
slug: payby-release-process-workflow
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:1c44fa5b-606f-4bee-876e-06c37345eb4d
tags: []
---

# PayBy发布流程状态流转

本页描述 PayBy Release Process 的两个层面：
1. Jira 任务的**状态机流转**（NEW TASK → COMPLETED / SECURITY COMPLETED）。
2. 围绕发布日的**协作时间线与职责分工**（QA Lead / QA / Dev / DBA / OPS）。

---

## 一、Jira 状态机

### 状态节点

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

### 主流程流转（UAT 阶段）

从 `NEW TASK` 起，依次顺序流转：

1. `NEW TASK` → `IN DEVELOPING`
2. `IN DEVELOPING` → `WAIT TEST`
3. `WAIT TEST` → `SIM TESTING`
4. `SIM TESTING` → `UAT DB CHANGE`
5. `UAT DB CHANGE` → `UAT DEPLOY`
6. `UAT DEPLOY` → `UAT TESTING`

`UAT TESTING` 完成后，流程切换到确认与生产部署阶段。

### 主流程流转（确认与生产阶段）

从 `UAT TESTING` 进入：

1. `UAT TESTING` → `SECURITY CONFIRM`
2. `SECURITY CONFIRM` → `TECH LEAD CONFIRM`
3. `TECH LEAD CONFIRM` → `QA LEAD CONFIRM`
4. `QA LEAD CONFIRM` → `PROD DB CHANGE`
5. `PROD DB CHANGE` → `PROD DEPLOY`
6. `PROD DEPLOY` → `PROD VERIFY`
7. `PROD VERIFY` → `COMPLETED`
8. `COMPLETED` → `SECURITY COMPLETED`

### 特殊路径

- **跳转路径**：`QA LEAD CONFIRM` 可直接跳转到 `PROD VERIFY`，跳过 `PROD DB CHANGE` 与 `PROD DEPLOY`。
- **回退路径**：标记为 `All` 的转移指向 `NEW TASK`，表示任意状态均可回退到 `NEW TASK`。
- **游离节点**：`MANAGER CONFIRM` 未与主流程连线。

### 终态标识

- `COMPLETED`：常规发布终态。
- `SECURITY COMPLETED`：在 `COMPLETED` 之后经安全确认到达的最终态。

---

## 二、发布日协作流程（T-1 与 Release Day）

发布节奏遵循 **MONDAY / WEDNESDAY = T-1（准备日）**，**TUESDAY / THURSDAY = Release Day（上线日）**。所有时间为 UTC+4。

### T-1：准备日（MONDAY / WEDNESDAY）

#### 1. 17:00 — QA Lead：敲定上线清单

- 确认上线日最终上线 Jira。
- 检查应用冲突。
- 检查 Jira 中 CR、配置规范。
- **交付物**：The Release JIRA List（上线 Jira List）。

#### 2. 17:30 — QA Lead：同步与归档

- 将初版上线 List 与上线时间同步至 DBA、OPS、Dev。
- 在上线 Teams 群中创建 **“Release confirmation Loop”** 频道。
- 创建 Wiki page **“YYYY-MM-DD Release Detail”** 记录上线 Jira。
- **交付物**：
  - Teams 上线 Jira List（形如 `https://algento.atlassian.net/browse/PAYM-XXXX`）
  - Teams Loop（确认 Loop）
  - “YYYY-MM-DD Release Detail” Wiki 文档

> **要点**：
> - 为避免上线群消息冲突，confirmation loop 在**新建的 Teams 群**中单独发送。
> - T-1 的上线 List **不是最终版本**，仅反映 QA 当前预期能按时上线的 Jira；最终可能因测试发现的问题或其他阻塞而被剔除。
> - **最终 List 在 Release Day 当天再次发出**。

#### 3. Release Jira Dev：Loop 确认

- 在上线 Teams 群中勾选确认上线。
- **交付物**：Teams Loop acknowledgement。

---

### Release Day：上线日（TUESDAY / THURSDAY）

#### 4. 06:00 — QA Lead：发出最终清单

- 在上线 Teams 群同步**最终上线 Jira List**。
- 创建 **“Online confirmation Loop”** 频道。
- **交付物**：Final Jira List、Teams Loop（确认 Loop）。

#### 5. QA：召集 Dev online 确认

- 在上线 Teams 群中 @ 项目开发，确认是否 online。

#### 6. Release Jira Dev：响应 online

- Dev 响应 QA，并在 Teams loop 中勾选 **“online confirmed”**。
- **交付物**：Teams Loop acknowledgement。

#### 7. QA：推进上线

- 根据 online loop 状态推进上线。
- 若存在 **before CR**，发布版本前 @ DBA。
- 发布版本时 @ OPS。
- 若存在 **after CR**，发布版本后 @ DBA。

> **要点**：若开发超过 **30 分钟**仍未 online，该项目将因 **“Dev not ready”** 取消上线。

随后由 QA Lead 在上线 Teams 群创建 **“CR/Config/LOG confirmation Loop”** 频道，用于发布后开发自检。

#### 8. DBA / OPS：执行并回执

- 执行完成后更新 Jira 状态，并上传执行结果。
- 在 Teams 群回复 QA。
- **交付物**：Jira 状态更新。

#### 9. Release Jira Dev：上线后自检

Dev 对上线结果进行检查：

- 如 Jira 中存在 **CR**，验证执行结果。
- 如 Jira 中存在 **Configuration**，验证结果。
- 检查应用日志。
- 关注相关监控/告警。
- 在 “CR/Config/LOG confirmation Loop” 中勾选确认已完成所有检查。
- **交付物**：Teams Loop acknowledgement。

#### 10. QA：生产验证

- 执行生产环境验证。
- 验证完成后将 Jira 状态更新为 **`COMPLETED`**。
- 若无法实时验证，需添加备注（comment）。

#### 11. Dev：双重检查

- 对生产交易进行
