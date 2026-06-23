---
title: PayBy 发布流程角色与职责
domain: payby-core-systems
kind: wiki_page
slug: payby-release-process-roles-responsibilities
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/1405976629
tags: []
---

# PayBy 发布流程角色与职责

本页按时间顺序详述 PayBy 发布周期内 QA Lead、Dev、DBA、OPS、QA 在每个节点的职责、交付物，以及通过 Teams Loop 进行的协作确认机制。整体节奏遵循 [[payby-release-process]] 的排期（T-1 准备日：周一/周三；上线日：周二/周四）。

## 阶段一：T-1 准备日（周一 / 周三）

### Step 1 — 17:00 (UTC+4)：QA Lead 锁定上线清单
- 确认上线日最终上线 Jira
- 检查应用冲突
- 检查 Jira 中 CR、配置规范
- 交付物：The Release JIRA List（上线 Jira List）

### Step 2 — 17:30 (UTC+4)：QA Lead 同步信息并建群建档
- 同步上线 List 及上线时间至 DBA、OPS、开发
- 在上线 Teams 群中创建 **Release confirmation Loop**
- 创建 Wiki page `YYYY-MM-DD Release Detail` 记录上线 Jira
- 交付物：
  - Teams 上线 JIRA List 消息
  - Teams Loop（确认 Loop）
  - Wiki page `YYYY-MM-DD Release Detail`
- 重点说明：
  - 为避免上线主群消息冲突，confirmation Loop 在**新建的 Teams 群**中单独发送
  - T-1 的上线 List **不是最终版**，仅反映 QA 当前预估可按时上线的 Jira；如发现新缺陷或其它阻塞项可能被剔除
  - 最终版上线日当天再次发送

### Step 3 — Release Jira Dev 在 Loop 中确认就绪
- 在 Teams Loop 中勾选确认上线
- 交付物：Teams Loop acknowledgement

## 阶段二：上线日早间确认（周二 / 周四）

### Step 4 — 06:00 (UTC+4)：QA Lead 发布最终清单
- 在上线 Teams 群中同步最终上线 Jira
- 创建 **Online confirmation Loop**（开发 online 确认 Loop）
- 交付物：Final Jira List、Teams Loop

### Step 5 — QA 触达开发
- 在上线 Teams 群中 @ 项目开发，确认是否 online

### Step 6 — Release Jira Dev 响应 online
- 响应 QA，并在 Teams Loop 中勾选确认已在线
- 交付物：Teams Loop acknowledgement

## 阶段三：发布执行

### Step 7 — QA 推进上线 + QA Lead 建检查 Loop
- QA 根据 online Loop 状态推进上线
- 如有 **before CR**：发布版本**前** @ DBA
- 发布版本时 @ OPS
- 如有 **after CR**：发布版本**后** @ DBA
- 重点说明：若开发超过 30 分钟仍未 online，该项目将以「Dev not ready」原因取消上线
- QA Lead：在上线 Teams 群中创建 **CR/Config/LOG confirmation Loop**
- 交付物：Teams Loop（确认 Loop）

### Step 8 — DBA / OPS 执行反馈
- 执行完成后更新 Jira 状态，并上传执行结果
- 在 Teams 群中回复 QA
- 交付物：Jira 状态已更新

### Step 9 — Release Jira Dev 上线后检查
- 如 Jira 存在 CR：核对执行结果
- 如 Jira 存在 Configuration：核对结果
- 检查应用日志
- 关注相关监控（dashboards / alerts）
- 在 Teams Loop **CR/Config/LOG confirmation Loop** 中勾选确认已完成所有检查
- 交付物：Teams Loop acknowledgement

## 阶段四：生产验证与收尾

### Step 10 — QA 生产验证
- 进行生产环境验证
- Jira 状态更新为 `COMPLETED`
- 如不能实时验证，添加 comment 备注

### Step 11 — Dev 双重检查
- 双重检查生产交易（Double-check production transactions）

### Step 12 — QA Lead 沉淀记录
- 更新当天上线情况至 Wiki，内容包括：
  - 最终验证结果（validation results）
  - 上线异常记录（anomalies logged）
  - Loop 确认结果（Loop outcomes）
- 交付物：Wiki page `YYYY-MM-DD Release Detail`

## Teams Loop 协作机制总览

整个流程围绕 **3 个独立的 Teams Loop** 串联，全部在新建的 Teams 群中单独发送，避免主群消息冲突：

| Loop 名称 | 创建时间 | 确认方 | 用途 |
|---|---|---|---|
| Release confirmation Loop | T-1 17:30 | Release Jira Dev | 确认按预估清单上线 |
| Online confirmation Loop | 上线日 06:00 | Release Jira Dev | 确认开发已 online |
| CR/Config/LOG confirmation Loop | 发布执行阶段 | Release Jira Dev | 确认 CR / 配置 / 日志 / 监控检查完成 |

## 关联流程

- 排期与时间窗口详见 [[payby-release-process]]
- 上线前协作流程参见：Pre-Release Dev-Test-Product Collaboration Process（SIM → UAT → Go-Live Checklist）
