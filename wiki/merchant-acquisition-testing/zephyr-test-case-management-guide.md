---
title: Zephyr 测试用例管理操作指南
domain: merchant-acquisition-testing
kind: wiki_page
slug: zephyr-test-case-management-guide
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:05965a2a-f4db-46cf-804d-a1d58b150364
tags: []
---

# Zephyr 测试用例管理操作指南

本文介绍如何在 Zephyr（Jira 插件）中维护测试用例库、组织 Test Cycle、执行测试并与 Jira 缺陷联动的完整操作流程。

## 核心概念

| 概念 | 说明 |
| --- | --- |
| Test Cases | 以测试用例库形式维护的独立用例 |
| Test Cycles | 针对某个测试任务挑选的一组用例集合；同一用例可存在于不同 Cycle 中，且各自拥有独立的执行状态与关联 Bug |

## 创建测试用例

支持两种方式：

- **方式 A：在 Zephyr 中手动创建**
  - 在 Zephyr 插件中填写用例详情
  - 必须选择 `Component` 和 `Priority`
- **方式 B：Excel 批量导入**
  - 在 Excel 中编写用例后批量导入
  - 推荐用于回归测试用例
  - 模板单独提供

## 创建 Test Cycle

按实际测试需要创建 Test Cycle，示例：

- APP Regression
- Merchant Transaction Regression
- Feature A Testing
- Feature B Testing

### 向 Cycle 添加用例

1. 点击 Test Cycle，再点击 Cycle key
2. 进入 `Test Cases` 标签页，点击 `Add Cases`
3. 从用例库中按顺序选择并添加

### 环境处理

- 用例本身不区分环境，需为不同环境分别创建 Test Cycle
- 示例：`Merchant place PAYPAGE order – SIM`、`Merchant place PAYPAGE order – UAT`、`Merchant place PAYPAGE order – PROD`

### 关联 Jira 发布任务

1. 在 Test Cycle 中点击 `Traceability`
2. 在 `Issues` 行最右侧点击放大镜搜索图标
3. 输入 Jira release ticket key 并回车
4. 关联后，Jira 页面会显示对应的 Test Cycle 及其执行进度

## 执行测试

1. 在 Test Cycle 中点击 `Test Player`
2. 点击右上角 Start 按钮，计时开始
3. 左侧 `Test Script` 显示测试步骤与预期结果，右侧记录执行结果
4. **执行前先选择环境**
5. 将每条用例标记为 Pass/Fail

### 发现 Bug 时

- 将执行结果设置为 `Fail`
- 提交结果，并直接在执行页面 `Create Bug`
- 在弹窗中填写 Bug 详情（字段同常规 Bug）
- 创建后的 Bug 会出现在 `Issues` 区域

### Bug 修复后的复测

- 选择该测试用例
- 点击 `Start a new test execution`，生成一条新的执行记录
- 重新执行该用例
- Jira 状态以**最终一次执行结果**为准
