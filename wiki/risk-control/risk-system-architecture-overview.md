---
title: 风控系统架构总览
domain: risk-control
kind: wiki_page
slug: risk-system-architecture-overview
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:00c6a300-c75b-4c5d-b0c9-c18e010dfb50
tags: []
---

# 风控系统架构总览

风控系统以 GRC 组件为请求入口，通过事件类型分流与持久化、双开关运行时控制、以及 IP 定位解析三大基础能力，支撑上层 Visual Rule 策略体系运转。

## GRC 组件与请求路径

- 核心组件：`gp079_grc-component-connect-provider`，承担 verifyRisk 请求路径上的接入与分发角色。
- 一次 `verifyRisk` 请求的典型链路：API ingress → GRC 组件处理 → 事件文档持久化。
- 相关接口与触发方式见 [[api_grc_verify_risk]] 与 [[risk-verifyrisk-firing-and-verification]]。

## 事件类型与持久化集合

GRC 接收的事件按类型落入不同 MongoDB 集合（按年份分表）：

- `PAYMENT`：支付类事件 → 写入 `grc.t_payment_event_<yyyy>`
- `ENTER_WALLET`：进入钱包事件 → 写入 `grc.t_other_event_<yyyy>`
- `CASHDESK_INIT`：收银台初始化事件 → 写入 `grc.t_other_event_<yyyy>`
- 身份类（identity）事件 → 写入 `grc.t_other_event_<yyyy>`

事件文档关键字段：`riskStatus`、`remoteIpInfo`、`trueIpInfo`、动作执行结果（action outcome）。

> 速记：`PAYMENT` 走 `t_payment_event_<yyyy>`，其余事件统一进 `t_other_event_<yyyy>`。

## 双开关模型（Apollo + aml.t_system_param）

风控运行态由两个独立开关层共同控制：

- **Apollo YAML 配置**
  - 构建/重启时生效（build / restart-time）
  - 修改后需要 Tomcat 重启才会加载，不可热更新
  - 适用于 kill switch 等需要确定性切换的开关
- **`aml.t_system_param` 运行时参数**
  - 运行期生效，可通过缓存刷新热更新
  - 缓存刷新路径：Basis → Function Query → Cache Clear → `gp079_grc-component-connect-provider` → `systemParam` Clear（必要时配合 `ip` Clear）
  - 仅在 "Risk Param page → Save" 不足以让新值真正生效，必须执行上述 Cache Clear 流程

回滚时的两条路径：
1. 通过 Visual Rule UI 直接 disable 规则（影响面最小）
2. 翻转 `aml.t_system_param` 标志位 + 执行缓存清理

## IP 定位解析（IP-area resolver）

系统存在两套 IP 定位实现，路径是否走新引擎可通过事件文档中的签名识别：

- **新路径**：MaxMind GeoIP MMDB
- **旧路径**：`Ip2location`（legacy）
- **路径签名**：通过事件文档中 `remoteIpInfo._id` 的形态判断本次请求实际命中哪条 IP 定位路径
- **日志特征**：`GeoIPOperaUtil` 仅在出错时打日志，正常路径不会留痕；判断 path engagement 应优先依赖 doc-shape 签名而非日志

相关参考：PAYM-2744 IP-Location Optimization spec。

## 数据库与管理后台

- MongoDB 库：`grc`、`aml`、`bigdata`（QA 需具备读权限）
- 风控可视化规则后台：Basis Admin（`uat.intra.azure.test2pay.com/bigdata-admin/`），见 [[auto_basis_visual_rule_admin]]
- 配套观测/审计平台：AstraShield、Kibana
- 账号与权限准备见 [[risk-onboarding-account-access]]

## 与上层规则体系的衔接

GRC 接入的事件最终在 Visual Rule 体系内被检查点匹配并触发动作；策略-检查点-规则的层级与可视化规则的编写、激活流程见：

- [[risk-visual-rule-hierarchy]]
- [[risk-visual-rule-authoring-guide]]
- [[risk-visual-rule-activation-workflow]]

整体学习路径参见 [[risk-onboarding-week1-plan]]。
