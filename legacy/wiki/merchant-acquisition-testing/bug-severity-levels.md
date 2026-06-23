---
title: BUG级别定义与管理规范
domain: merchant-acquisition-testing
kind: wiki_page
slug: bug-severity-levels
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/2043740269
tags: []
---

# BUG级别定义与管理规范

本页定义 QA 团队在商户收单测试场景下的 BUG 严重级别（P0–P3）划分标准、发布前处理要求及特殊类别说明。

## 级别总览

| 级别 | 名称 | 发布前处理 |
|---|---|---|
| P0 | Critical (严重) | Must be fixed before release |
| P1 | High / Major (高级) | Should be fixed before release |
| P2 | Medium (中级) | 可延期修复，需产品/项目确认后放入遗留BUG |
| P3 | Low (低级) | 可延期修复，需产品/项目确认后放入遗留BUG |

## P0 — Critical Bug（严重）

发布前必须修复，属于 showstopper 级别问题：

- 导致系统完全无法工作
- 导致数据损坏或数据丢失
- 导致金钱损失
- 影响大量用户
- 影响 VIP 用户或关键业务客户

## P1 — Major Bug（高级）

发布前应当修复，影响主要功能或阻塞测试推进：

- 导致某些重要功能无法正常工作
- 影响系统核心功能
- 阻塞主流程或关键业务流程
- 阻止测试人员或团队继续测试与发布

## P2 — Medium Bug（中级）

修复可延后，但需与产品/PM 联合确认后才能作为遗留 BUG 暂时接受：

- 主要影响日常功能和次要缺陷
- 不影响主流程及重要功能

## P3 — Low Bug（低级）

修复可推迟，需经产品/项目确认后放入遗留 BUG：

- 打字错误（Typo）
- 措辞 / 文案微调
- 非核心功能的小缺陷
- 不显著影响用户体验的 UI 不一致问题

## 其他类别

### 优化建议
- 针对产品设计、用户体验提出的意见和建议
- 处理方式：指向（转交）产品团队

### Silly Bug
明显不应发生、暴露质量意识问题的 bug，典型表现：

- Reopen 次数过多
- 明面上一眼能看出来的问题
- 自测时未核对 UI 设计图
- 代码合并错误导致的问题

## 发布前处理要求小结

- **必须修复**：P0
- **应当修复**：P1
- **可作为遗留 BUG（需产品/项目确认）**：P2、P3
- **不计入 BUG 修复范围**：优化建议（转产品）

> 相关：[[bug-severity-levels]]
