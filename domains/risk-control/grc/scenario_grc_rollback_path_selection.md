---
id: scn_grc_rollback_path_selection
object_type: Scenario
domain: risk-control
status: active
owner: consolidation
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-22'
source_type: consolidation
source_ref: consolidation:risk-control:b4
tags:
- rollback
- killswitch
- system-param
subdomain: grc
module: null
sensitivity: normal
name: 风控规则回滚路径选择
aliases: []
related_services:
- svc_grc_component_connect_provider
related_tables:
- tbl_aml_t_system_param
related_scenarios:
- scn_grc_apollo_killswitch_restart_required
- scn_grc_system_param_cache_refresh
related_logs: []
related_requirements: []
related_failures: []
---

## 触发/入口
风控规则上线后出现问题需要回滚，决定采用何种回滚手段。

## 前置条件
- 已识别问题规则或问题配置项。
- 已评估影响范围（blast radius）。
- 了解双开关模型：Apollo YAML（构建/重启时生效，非热更新）与 `aml.t_system_param`（运行时生效，可通过缓存刷新）。

## 操作步骤
按 blast radius 在两种回滚方案中择一：

1. **UI 禁用规则**
   - 在 Basis Admin 直接将问题规则下线/禁用。
   - 适用于影响范围局限于单条规则的情况。

2. **翻转 `aml.t_system_param` 标志位 + 清缓存**
   - 在 `aml.t_system_param` 中翻转对应标志位。
   - 通过 Basis → Function Query → Cache Clear → `gp079_grc-component-connect-provider` → `systemParam` Clear 刷新缓存。
   - 注意：仅在 Risk Param 页点 Save 不足以让新值生效，必须走缓存清理流程。
   - 适用于需要通过运行时参数批量控制的情况。

## DB 校验点
- `aml.t_system_param`：确认目标标志位已被翻转为期望值。

## 预期结果
- 选定的回滚路径生效后，问题规则或配置不再影响线上请求。
- 若涉及 Apollo Kill Switch 类配置，则不属于本回滚路径（非热更新，需重启后验证）。
