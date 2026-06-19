---
title: Visual Rule 创建与编写指南
domain: risk-control
kind: wiki_page
slug: risk-visual-rule-authoring-guide
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:00c6a300-c75b-4c5d-b0c9-c18e010dfb50
tags: []
---

# Visual Rule 创建与编写指南

本页讲解如何在 Basis 后台从零创建一条 Visual Rule：先建测试策略并绑定检查点，再在策略下编写 `oneRow` / `mostRow` 两类 `ADD_TO_LIST` 规则，最后保存为 `DRAFT`。规则层级、激活流程与触发验证见 [[risk-visual-rule-hierarchy]] 与 [[risk-visual-rule-activation-workflow]]。

## 创建测试策略

- 在 Strategy Manager 创建一个测试策略，配置 folder、status、effective time
- 可参考既有测试策略 `FT_PAYM2755_TEST`
- 将策略绑定到检查点（例如 `FT Add to list`、`FT_ATL_CP`）
- 确认该检查点接的是真实 CGS 事件源，而不是仅供测试

## 策略版本部署陷阱

- 一个策略只有 **唯一一个** 已部署版本
- 挂在「未部署版本」下的规则**不会**在真实事件上触发
- 多版本策略必须明确识别当前 deployed version；新建/修改规则前先确认自己挂的是 deployed 那一版

## 编写 Visual Rule

在自己的策略下新建一条 Visual Rule：

- 配置条件：基于事件字段、比较运算符、AND/OR 分组
- 配置 `ADD_TO_LIST` 动作，分两种行写入模式：
  - `oneRow`：单个 `[type, value]` 对
  - `mostRow`：多列行（按 `fieldDef` 列拼装）
- 通过 Fields 下拉选择字段，下拉项受限于：
  - `oneRow` 规则：`listRepoFieldType`
  - `mostRow` 规则：列表仓的 `fieldDef` 列
- 为目标 list repo 选对仓库（如 `LAF_blocklist`、`LAF_appeal_acceptlist` 等）
- 编写完成后保存为 `DRAFT`

list repo 与字典定义（`bigdata_list_repo` 的 `listRepoAttr` / `fieldDef`、`bigdata_system_dic` 的 `addListRepos` / `listRepoFieldType`、3 列上限）见 [[risk-visual-rule-hierarchy]]。

## 字段精确匹配契约

- UI 上 EN/ZH tooltip 已说明：**payload 字段名必须与列的 field 名完全一致**
- **大小写敏感**，**没有任何自动映射**
- 字段名拼错 = 规则不命中。排查"规则没触发"时，字段名 mismatch 是首位嫌疑

## oneRow vs mostRow 的部分空值语义

写入时若个别字段为空，两种模式行为不同：

- `oneRow`：静默跳过那一条空 attr，其他正常写入
- `mostRow`：**整行**写入被中止

所以 `mostRow` 规则的列选择必须满足该 list repo 的 `fieldDef` 全列可填。

## 产出物（Day 3）

- 在自有测试策略下，至少各完成一条 `oneRow` 与 `mostRow` 的 `DRAFT` 规则
- 能解释「为什么这个列选择对该 repo 的 `fieldDef` 是合法的」
- 能口头描述 Strategy → Checkpoint → Rule 层级

## 后续步骤

- 把 `DRAFT` 推上线：见 [[risk-visual-rule-activation-workflow]]
- 触发 `verifyRisk` 校验规则命中：见 [[risk-verifyrisk-firing-and-verification]]
- 操作后台与接口：[[auto_basis_visual_rule_admin]]、[[api_grc_verify_risk]]
