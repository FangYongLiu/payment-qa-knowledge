---
title: Visual Rule 策略-检查点-规则体系
domain: risk-control
kind: wiki_page
slug: risk-visual-rule-hierarchy
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:00c6a300-c75b-4c5d-b0c9-c18e010dfb50
tags: []
---

# Visual Rule 策略-检查点-规则体系

Basis 风控可视化规则按 **Strategy → Checkpoint → Rule** 三层组织,配合 List Repo 与系统字典支撑 Action 落地。本页梳理这一层级模型与关键概念,作为 [[risk-visual-rule-authoring-guide]] 与 [[risk-visual-rule-activation-workflow]] 的前置知识。

## 三大规则形态

在 Basis 管理后台([[auto_basis_visual_rule_admin]])上并存三类规则视图:

- **Visual Rules** — 可视化规则,本页核心对象
- **Group Rules** — 规则组
- **Strategy Set** — 策略集合

## Strategy → Checkpoint → Rule 层级

- **Strategy(策略)**:顶层容器,具备 folder、status、effective time 等属性,有版本概念(同一策略仅一个版本被部署生效)
- **Checkpoint(检查点)**:策略绑定到具体业务事件源的接入点(例如 `FT Add to list`、`FT_ATL_CP`),需要确认是真实 CGS 事件源还是仅测试用
- **Rule(规则)**:挂在策略下的最小执行单元,包含条件(event 字段、比较、AND/OR 分组)与 Action

事件类型(`PAYMENT`、`ENTER_WALLET`、`CASHDESK_INIT`、identity events 等)由 Checkpoint 对接,具体触发参见 [[risk-verifyrisk-firing-and-verification]]。

## Action 类型

Visual Rule 支持的 Action 包含:

- `ADD_TO_LIST` — 写入名单库(List Repo)
- `REJECT`
- `REVIEW`
- `PASS`
- value-set actions
- 其他

其中 `ADD_TO_LIST` 的写入形态由目标 List Repo 的 `listRepoAttr` 决定。

## List Repo:`oneRow` vs `mostRow`

List Repo 数据存储在 MongoDB 集合 `bigdata_list_repo` 中,关键属性:

- **`listRepoAttr`**:决定行结构
  - `oneRow` — 单 `[type, value]` 对,每条记录就是一个属性键值
  - `mostRow` — 多列行,字段由 `fieldDef` 定义
- **`fieldDef`**:`mostRow` 模式下的列定义
- **3-column cap**:`mostRow` 列数上限为 3

典型 List Repo 示例:`LAF_blocklist`、`LAF_appeal_acceptlist`。

### 字段下拉与匹配语义

在编写 `ADD_TO_LIST` 规则时,Fields 下拉的过滤来源:
- `oneRow` → 由系统字典 `listRepoFieldType` 过滤
- `mostRow` → 由该 Repo 的 `fieldDef` 列过滤

**字段名严格匹配**:payload 字段名必须与列字段名 **大小写完全一致**,系统不做自动映射(EN/ZH tooltip 强调此点)。

### 部分空值语义

- `oneRow` — 静默跳过空的 attr,其余正常写入
- `mostRow` — 任一列空值则整行写入中止

## 系统字典(`bigdata_system_dic`)

支撑 List Repo 行为校验的关键字典项:

- **`addListRepos`** — 合法 `repoNo` 白名单;被篡改的未知 `repoNo` POST 会被拒绝
- **`listRepoFieldType`** — `oneRow` 模式下可选字段类型来源

热删除的目标 List Repo 触发规则时表现为优雅 no-op + 日志,而非抛异常。

## 相关页面

- 规则编写实操 → [[risk-visual-rule-authoring-guide]]
- 规则上线流程 → [[risk-visual-rule-activation-workflow]]
- 触发与落库验证 → [[risk-verifyrisk-firing-and-verification]]
- 系统全景 → [[risk-system-architecture-overview]]
