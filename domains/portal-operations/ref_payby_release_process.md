---
id: ref_payby_release_process
object_type: reference
name: PayBy 发布流程与排期
aliases: [payby release process, 发布流程, release schedule, definition of done]
domain: portal-operations
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: 'wiki_image:16bef575-8173-4c56-857e-6a52c9d1f8a3'
tags: [release, process, deploy, qa, dod]
related_services: []
---

# PayBy 发布流程与排期

> PayBy 常规发布窗口为每周二、周四 UAE 时间 06:00;窗口外的 Hotfix 必须经管理团队严格审批。本页为 QA/DEV/DevOps 协作的发布流程参考。

## 常规发布窗口
- 每周二 06:00(UAE);每周四 06:00(UAE)。
- 窗口外 Hotfix 走管理团队严格审批。

## 周排期(Release 1 / Release 2，含上周 Release 0 收尾)
- **周一**:R0 UAT 部署/测试;R2 QA SIM 测试。
- **周二**:R0 PROD 部署/验证;R1 SIM + QA SIM 测试、Scope & Config Review、DEV Merge to Master(Cutoff)。
- **周三**:R1 UAT 部署 + QA UAT 测试;R2 QA SIM 测试。
- **周四**:R1 PROD 部署 + QA PROD 验证;R2 QA SIM 测试、Scope & Config Review、DEV Merge to Master(Cutoff)。
- **周五/六/日**:无固定发布活动。

## 角色与职责
- **DevOps / DBA**:UAT 与 PROD 部署;依据 release scoped ticket 的 Build Version、CRs、Configuration files 执行。**所有 UAT 部署与配置变更仅限 DevOps/DBA**。
- **QA**:在 SIM/UAT/PROD 做 Functional/Regression/Smoke(手工+自动化)。
- **DEV**:DEV 自测;QA SIM 通过后合 master;发布前对各自 ticket 完成 **Confirm CR / Config / Log** 任务(Internal 可见，Due=发布当日)。

## 工作流新增状态
- `UAT DB CHANGE`、`UAT DEPLOY`(配合 UAT 变更仅 DevOps/DBA 执行)。
- **安全确认流程**(涉及暴露公网的核心服务变更):UAT QA 验证后切 `SECURITY CONFIRM`，最终结束状态为 `SECURITY COMPLETED`(而非普通 `COMPLETED`)。

## Definition of Done
- 所有 ticket 上线 PROD，状态 `COMPLETED` 或 `SECURITY COMPLETED`。
- 各 ticket 的 Confirm CR / Config / Log 任务由对应 Dev 完成。
- 部署过程问题需复盘:分析 root cause + action items，避免重复。
