---
title: PayBy 发布流程与排期
domain: payby-core-systems
kind: wiki_page
slug: payby-release-process
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/1405976629
tags: []
---

# PayBy 发布流程与排期

PayBy 常规发布窗口为每周二、周四 UAE 时间 06:00。任何在常规发布窗口之外的 Hotfix 部署都必须经过管理团队的严格审批流程。

## 常规发布窗口

- 每周二 06:00 (UAE Time)
- 每周四 06:00 (UAE Time)
- 窗口外的 Hotfix 需走管理团队严格审批

## 周排期

按一周排布两个发布序列（Release 1 与 Release 2），并保留上一周的 Release 0 收尾活动。

**MONDAY**
- Release 0 - UAT DEPLOYMENT
- Release 0 - UAT TESTING
- Release 2 - QA SIM TESTING

**TUESDAY**
- Release 0 - PROD DEPLOYMENT
- Release 0 - PROD VALIDATION
- Release 1 - SIM TESTING
- Release 1 - QA SIM TESTING
- Release 1 - Release scope and Config Review
- Release 1 - DEV Merge to Master (Cutoff Time)

**WEDNESDAY**
- Release 1 - UAT DEPLOYMENT
- Release 1 - QA UAT TESTING
- Release 2 - QA SIM TESTING

**THURSDAY**
- Release 1 - PROD DEPLOYMENT
- Release 1 - QA PROD VALIDATION
- Release 2 - QA SIM TESTING
- Release 2 - Release scope and Config Review
- Release 2 - DEV Merge to Master (Cutoff Time)

**FRIDAY / SA / SU**
- 无固定发布活动

## 角色与职责

详细的角色分工与跨团队协作清单见 [[payby-release-process-roles-responsibilities]]。

**DEVOPS / DBA**
- 负责 UAT 与 PROD 的部署
- 依据 release scoped tickets 中的信息执行：Build Version、CRs、Configuration files 等
- 所有 UAT 部署与配置变更仅限 DevOps 与 DBA 团队执行

**QA**
- 在 SIM、UAT、PROD 进行测试：Functional Testing、Regression、Smoke
- 覆盖手工与自动化两种方式

**DEV**
- 在 DEV 环境完成 Self Tests
- 在 QA 完成 SIM 测试后，将代码合并到 master

## 工作流新增状态

整体流程中新增两个状态，配合"UAT 部署与配置变更仅由 DevOps/DBA 执行"的规范：

- `UAT DB CHANGE`
- `UAT DEPLOY`

## 安全确认流程

针对涉及暴露到公网的核心服务变更的 ticket：

- 在 UAT 完成 QA 验证后，需要将状态切换为 `SECURITY CONFIRM`
- 最终结束状态为 `SECURITY COMPLETED`，而不是普通的 `COMPLETED`

## 发布日协作时间线（T-1 与 Release Day）

发布按"T-1 准备日（MONDAY / WEDNESDAY）"与"上线日（TUESDAY / THURSDAY）"两阶段推进。所有确认动作通过 Teams 的 Loop 完成。

### T-1（MONDAY / WEDNESDAY）

**17:00 (UTC+4) — QA Lead 准备初版上线清单**
- 确认上线日最终上线 Jira
- 检查应用冲突
- 在 Jira 中校验 CR 与配置规范
- 交付物：The Release JIRA List

**17:30 (UTC+4) — QA Lead 同步信息**
- 将初版上线 List 与上线时间同步至 DBA、OPS、Dev
- 在上线 Teams 群中创建 "Release confirmation Loop"
- 创建 Wiki page `YYYY-MM-DD Release Detail` 归档上线 Jira
- 注意：为避免与主发布群消息冲突，Confirmation Loop 在新建的 Teams 群中单独发布
- 注意：T-1 发出的清单**不是最终版**，仅代表 QA 当前预估可按时上线的 Jira；如发现新缺陷或其他阻塞，仍可能被剔除，最终清单在上线日当天重新发出

**Release Jira Dev 确认**
- 在 Teams Loop 中勾选确认上线就绪

### 上线日（TUESDAY / THURSDAY）

**06:00 (UTC+4) — QA Lead 发布最终清单**
- 在上线 Teams 群中同步最终上线 Jira List
- 创建 "Online confirmation Loop" 用于开发 online 确认

**Online 确认**
- QA 在 Teams 群中 @ 对应项目开发确认是否 online
- Dev 响应 QA 并在 Loop 中勾选 "online confirmed"
- 规则：若开发超过 30 分钟仍未 online，该项目将以 "Dev not ready" 取消上线

**推进部署**
- QA 根据 Online Loop 状态推进上线
- 如存在 **before CR**：发布版本前 @ DBA
- 发布版本时 @ OPS
- 如存在 **after CR**：发布版本后 @ DBA
- QA Lead 在 Teams 群中创建 "CR/Config/LOG confirmation Loop"

**DBA / OPS 执行反馈**
- 执行完成后更新 Jira 状态并上传执行结果
- 在 Teams 群中回复 QA

**Dev 检查上线结果**
- 如 Jira 存在 CR，检查执行结果
- 如 Jira 存在配置变更，检查配置结果
- 检查应用日志
- 关注相关监控/告警
- 在 "CR/Config/LOG confirmation Loop" 中勾选确认完成所有检查

**生产验证**
- QA 进行生产环境验证，将 Jira 状态更新为 `COMPLETED`（如不能实时验证，添加备注）
- Dev 双重检查生产交易

**收尾**
- QA Lead 将当天上线情况更新至 Wiki page `YYYY-MM-DD Release Detail`，包括最终结果、上线异常记录、Loop 确认结果

## Definition of Done

- 所有 ticket 已上线 PROD，且状态为 `COMPLETED` 或 `SECURITY COMPLETED`
- 当天 Wiki page `YYYY-MM-DD Release Detail` 已更新最终结果、异常记录与 Loop 确认结果
- 部署过程中出现的任何问题都需复盘，分析 root cause，并制定 action items，避免后续重复发生

## 相关流程

- Pre-Release Dev-Test-Product Collaboration Process (SIM → UAT → Go-Live Checklist)
- PayBy Pre-Release Dev-Test-Product Collaboration Process (Channel)
