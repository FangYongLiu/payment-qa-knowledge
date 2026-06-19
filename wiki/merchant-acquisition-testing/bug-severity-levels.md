---
title: BUG级别定义与管理规范
domain: merchant-acquisition-testing
kind: wiki_page
slug: bug-severity-levels
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:ab63f7a0-100c-48e4-b9df-c7069abe2759
tags: []
---

# BUG级别定义与管理规范

本页定义测试过程中 BUG 的严重级别（P0–P3）、判定标准、修复时机，以及遗留 BUG 的确认流程。

## 级别一览

| 级别 | 名称 | 定义要点 | 备注 |
|---|---|---|---|
| P0 | Critical (严重) | 系统无法工作；数据损坏；金钱损失；大量客户受影响；VIP 使用受影响 | 发布前必须修复 |
| P1 | High (高级) | 某些重要功能无法正常工作；影响系统核心功能；主流程无法跑通；阻止测试或发布 | 发布前应修复 |
| P2 | Medium (中级) | 日常功能和大多数缺陷（不影响主流程及重要功能） | 须项目或产品确认后才能放入遗留 BUG |
| P3 | Low (低级) | 打字错误；措辞更改；不太重要的功能缺陷；UI 问题（不会严重影响用户体验） | 须项目或产品确认后才能放入遗留 BUG |
| — | 优化建议 | 对产品设计、用户体验的意见和建议 | 指向给产品 |
| — | Silly Bug | 比较傻的 bug | Reopen 次数过多；一眼能看出来的；自测未核对 UI 设计图的；代码合并错误的 |

## P0 — Critical Bug

发布前必须修复（Must be fixed before release）。属于 showstopper，严重影响系统功能或用户信任：

- 导致系统完全无法工作
- 导致数据丢失或损坏
- 造成金钱损失
- 影响大量用户
- 影响 VIP 用户或关键业务客户

## P1 — Major Bug

发布前应当修复（Should be fixed before release）。影响主要功能或阻塞测试的重大问题：

- 阻止部分关键功能正常工作
- 影响系统核心功能
- 阻塞重要用户流程或业务流程
- 阻止测试人员或团队推进测试或部署

## P2 — Medium Bug

修复可延后，需产品团队确认（Fix can be deferred, requires product team confirmation）。

- 主要影响次要功能
- 不影响关键流程或主要功能
- 与 Product/PM 联合确认后可临时接受

## P3 — Low Bug

修复可推迟，需产品团队确认（Fix can be postponed, requires product team confirmation）。

- 打字错误（Typographical errors）
- 文案/措辞细微修改
- 非核心功能问题
- 不显著影响用户体验的 UI 不一致

## 遗留 BUG 确认流程

- P0 / P1：不可遗留，发布前必须/应当完成修复
- P2 / P3：仅在项目或产品确认后才能放入遗留 BUG
- 优化建议：不计入 BUG，转交产品处理

## Silly Bug 判定

用于标记本应在自测/合并阶段拦截的低级问题，典型情形：

- Reopen 次数过多
- 明面上一眼能看出来的问题
- 自测未核对 UI 设计图
- 代码合并错误
