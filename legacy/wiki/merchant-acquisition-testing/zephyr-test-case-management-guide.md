---
title: Zephyr 测试用例管理操作指南
domain: merchant-acquisition-testing
kind: wiki_page
slug: zephyr-test-case-management-guide
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/2042429497
tags: []
---

# Zephyr 测试用例管理操作指南

Zephyr 是 Jira 的测试用例管理与执行插件，本页说明在 Zephyr 中创建用例、组织测试周期、执行用例并关联缺陷的操作流程。

## 核心概念

| 概念 | 说明 |
|---|---|
| Test Cases | 以测试用例库形式维护的独立测试用例 |
| Test Cycles | 为特定测试任务挑选的一组测试用例集合；同一测试用例可存在于不同 Cycle 中，状态与关联 Bug 相互独立 |

## 创建测试用例 (Test Cases)

两种方式：

- **方式 A：在 Zephyr 中手动创建**
  - 在 Zephyr 插件中填写用例详情
  - 必填项：必须选择 `Component` 和 `Priority`
- **方式 B：Excel 批量导入**
  - 在 Excel 中编写用例后批量导入
  - 推荐用于回归测试用例
  - 模板单独提供

## 创建 Test Cycles

按实际测试需求创建 Test Cycle，例如：

- APP Regression
- Merchant Transaction Regression
- Feature A Testing
- Feature B Testing

### 向 Cycle 添加用例

1. 点击 Test Cycle，再点击 Cycle key
2. 进入 `Test Cases` 标签页，点击 `Add Cases`
3. 从用例库中按顺序选择并添加

### 环境处理

- 测试用例本身不带环境概念，需为不同环境分别创建独立的 Test Cycle
- 示例：`Merchant place PAYPAGE order – SIM`、`Merchant place PAYPAGE order – UAT`、`Merchant place PAYPAGE order – PROD`

### 关联 Jira 发布单

1. 在 Test Cycle 中点击 `Traceability`
2. 在 `Issues` 行最右侧点击搜索图标（放大镜）
3. 输入 Jira 发布单 key 并回车
4. 关联后，Jira 页面会显示关联的 Test Cycle 及执行进度

## 执行测试

1. 在 Test Cycle 中点击 `Test Player`
2. 点击右上角 Start 按钮，计时开始
3. 左侧 `Test Script` 展示测试步骤与预期结果，右侧记录执行结果
4. 执行前先选择环境
5. 逐条标记 Pass / Fail

### 发现 Bug 时

- 将执行结果置为 `Fail`
- 提交结果，并直接在执行页 `Create Bug`
- 在弹窗中填写 Bug 详情（字段同常规 Bug）
- 创建后的 Bug 会显示在 `Issues` 区域

### Bug 修复后回归

1. 选中该测试用例
2. 点击 `Start a new test execution`，生成新的执行记录
3. 重新执行用例
4. Jira 状态以**最终一次执行结果**为准
