---
title: 风控缓存清理与Kill Switch操作
domain: risk-control
kind: wiki_page
slug: risk-cache-clear-and-killswitch
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/2161541121
tags: []
---

# 风控缓存清理与Kill Switch操作

本页汇总风控规则发布后运行期的缓存刷新路径、Kill Switch 触发方式、Trial 模式短路行为，以及按影响范围排序的回滚路径。

## 双开关模型回顾

风控引擎存在两层开关：

- **Apollo YAML**：build/restart 期生效，不可热加载。
- **`aml.t_system_param`**：运行期可通过缓存刷新生效。

> Kill Switch 与缓存刷新分别作用于不同层；选择哪一条路径取决于改动落在哪一层。

## 缓存清理操作路径

运行期（`aml.t_system_param` 一类）的参数变更，仅在 Risk Param 页 Save 是**不充分**的，必须执行清缓存动作。

操作位置：

- Basis → **Function Query** → **Cache Clear**
- 选择目标服务：`gp079_grc-component-connect-provider`
- 触发两个清理项：
  - `systemParam` Clear
  - `ip` Clear

规则发布侧另有约 **35s** 的缓存重载窗口，规则 ENABLED 后需等待该窗口才会真正生效（参见 [[risk-visual-rule-activation-workflow]]）。

## Kill Switch（Tomcat 重启型）

- Kill Switch **不是热加载**的，需要 **Tomcat 重启**才能生效。
- 验证时机：**重启之后**再确认，不要在重启前立即判断。
- 适用场景：Apollo YAML 层或需要进程重启的开关。

## Trial 模式短路

Trial 是一种"软关闭"机制，可在不真正动作的前提下观察规则是否命中：

- Trial 模式下规则**只写一行日志**，**不执行 action**（例如不会真正 `ADD_TO_LIST`）。
- 验证方式：通过 **list repo 中相应行的缺失**来确认未执行。
- Trial 短路在**规则级**与**策略级****各自独立**生效。

## 回滚路径（按影响半径排序）

从最小爆炸半径到最大：

1. **通过 Visual Rule UI 禁用单条规则** —— 最小范围，仅影响该规则。
2. **翻转 `aml.t_system_param` 标志位 + 执行缓存清理**（`systemParam` + `ip`）—— 影响该参数控制的整段逻辑。
3. **Kill Switch + Tomcat 重启** —— 最大范围，影响整个 GRC 组件层。

练习建议：在 sandbox 规则（DRAFT 阶段规则即可）上把以上路径都跑一遍。

## 排错切入点

- 改完参数没生效 → 先确认是否走过 Cache Clear，而不是只点了 Save。
- 规则没触发 action 但有日志 → 检查是否仍在 Trial 模式（规则级或策略级）。
- 改完 Kill Switch 立刻验证无效 → 检查 Tomcat 是否已重启。

更多自查项参见 [[risk-troubleshooting-checklist]]；规则触发与验证的端到端动作参见 [[risk-rule-firing-and-verification]]。
