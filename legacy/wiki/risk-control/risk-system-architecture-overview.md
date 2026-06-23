---
title: GRC风控系统架构总览
domain: risk-control
kind: wiki_page
slug: risk-system-architecture-overview
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/2161541121
tags: []
---

# GRC风控系统架构总览

本页梳理风控引擎的整体组件结构、事件分类与持久化、双层开关模型，以及 IP 归属解析的新旧两条路径，作为理解 verifyRisk 请求全链路的基础。

## 核心组件

- **GRC 组件**：`gp079_grc-component-connect-provider`，位于风控请求链路的核心位置，负责承接 verifyRisk 请求并驱动规则引擎。
- 上游入口：`verifyRisk` API（详见 [[api_grc_verify_risk]]）。
- 配套管理面：Basis Admin（`uat.intra.azure.test2pay.com/bigdata-admin/`）、AstraShield、Kibana、MongoDB（读 `grc` / `aml` / `bigdata` 库）。

## 事件类型与持久化集合

GRC 按事件类型路由到不同 MongoDB 集合（按年份分表）：

| 事件类型 | 持久化集合 |
|---|---|
| `PAYMENT` | `grc.t_payment_event_<yyyy>` |
| `ENTER_WALLET` | `grc.t_other_event_<yyyy>` |
| `CASHDESK_INIT` | `grc.t_other_event_<yyyy>` |
| identity 类事件 | `grc.t_other_event_<yyyy>` |

事件文档中关键字段：`riskStatus`、`remoteIpInfo`、`trueIpInfo`，以及命中规则后的 action outcome。

## 双开关模型

风控系统使用两层独立的开关控制，二者性质不同：

- **Apollo YAML（构建/重启时生效）**
  - 构建期或 Tomcat 重启时加载。
  - Kill Switch 类配置走这条路径——**非热更新**，改完必须等重启后再验证，不要立即下结论。
- **`aml.t_system_param`（运行时生效）**
  - 运行时配置，可通过缓存刷新生效。
  - 刷新方式：Basis → Function Query → Cache Clear → `gp079_grc-component-connect-provider` → `systemParam` Clear（+ `ip` Clear，见下节）。
  - 注意：仅在 Risk Param 页点 Save 不足以让新值生效，必须走缓存清理流程，详见 [[risk-cache-clear-and-killswitch]]。

回滚路径选择：UI 禁用规则 vs 翻转 `aml.t_system_param` 标志位 + 清缓存，按 blast radius 选择。

## IP-area 解析（新旧双路径）

verifyRisk 请求通过 Header `X-Forwarded-For` 携带 IP，由 GRC 解析归属地，存在两条解析路径：

- **旧路径：`Ip2location`**（legacy）
- **新路径：MaxMind GeoIP MMDB**（PAYM-2744 IP-Location Optimization）

**路径识别（path engagement signature）**：通过事件文档中 `remoteIpInfo._id` 的形态判断本次请求实际走的是哪条路径——这是判定新旧引擎是否生效的可靠手段。

**日志特征**：`GeoIPOperaUtil` 仅在出错时打日志，不能依赖日志确认路径是否生效，应以事件文档结构签名为准。

## 一次 verifyRisk 请求的链路概览

1. 请求经 API 入口进入 GRC 组件 `gp079_grc-component-connect-provider`。
2. 解析 `X-Forwarded-For` → 走 GeoIP 或 legacy IP2location 写入 `remoteIpInfo` / `trueIpInfo`。
3. 按 event type 命中策略 / Checkpoint，执行规则（参见 [[risk-visual-rule-authoring-guide]]）。
4. 事件文档落库到对应 `t_payment_event_<yyyy>` 或 `t_other_event_<yyyy>` 集合，附带 `riskStatus` 与 action outcome。
5. 触发与验证细节见 [[risk-rule-firing-and-verification]]。

## 相关页面

- 规则创作：[[risk-visual-rule-authoring-guide]]
- 激活流程：[[risk-visual-rule-activation-workflow]]
- 触发与验证：[[risk-rule-firing-and-verification]]
- 缓存清理与 Kill Switch：[[risk-cache-clear-and-killswitch]]
- 排错自查：[[risk-troubleshooting-checklist]]
