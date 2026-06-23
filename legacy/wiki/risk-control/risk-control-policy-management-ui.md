---
title: 风控策略管理后台界面说明
domain: risk-control
kind: wiki_page
slug: risk-control-policy-management-ui
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:0572f97e-d69b-4331-b776-2ac31d103069
tags: []
---

# 风控策略管理后台界面说明

本页描述 [[auto_dataeden_admin]] 中"策略管理"页面的整体布局、筛选条件与列表字段，便于快速定位和维护风控策略。

## 页面入口与操作按钮

- 页面标题：**策略**
- 右上角操作：
  - 新建策略
  - 新建策略目录（按钮文案被截断显示为"新建策略目..."）

## 筛选与搜索

顶部筛选区包含三个条件 + 搜索按钮：

- 策略编号：文本输入
- 状态：下拉，示例值 `ENABLED`
- 运行状态：下拉，示例值 `EFFECTIVE`
- 搜索按钮（带放大镜图标）

## 左侧目录树

策略以目录树形式组织，节点示例：

- TEST001（展开态，包含 TEST-003、TEST-004）
- TEST-002
- AF
  - ATO
  - SCC → SCCCC、SCCCC_002、SCCC_003
- AML
  - AML - type001

## 策略列表字段

主表格列（从左到右）：

| 列名 | 含义 |
|---|---|
| 所属目录 | 策略所在目录 |
| 策略编号 | Policy ID |
| 策略描述 | Description |
| 接入点 | Entry Point |
| 优先级 | Priority |
| 状态 | Status（如 `ENABLED`） |
| 运行状态 | Running Status（如 `EFFECTIVE`） |
| 对手策略 | Counter Policy |
| 规则数 | Rule Count |
| 最后修改人 | Last Modified By |
| 最后修改时间 | Last Modified Time |
| 操作 | 行级操作入口 |

## 数据示例

目录 TEST001 下的示例行：

1. **CT0005** — 策略-支付事件反欺诈，接入点 `[CP-GR-000002]`，优先级 1，状态 `ENABLED`，运行状态 `EFFECTIVE`，对手策略为空，规则数 11，最后修改人 daijinfeng，最后修改时间 Nov 9, 2022 1:13:42 PM
2. **CTTEST 1227** — 策略-测试1227，接入点 `[CP-GR-000002]`，优先级 1
