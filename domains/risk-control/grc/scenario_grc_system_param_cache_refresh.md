---
id: scn_grc_system_param_cache_refresh
object_type: Scenario
domain: risk-control
status: active
owner: consolidation
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-22'
source_type: consolidation
source_ref: consolidation:risk-control:b4
tags:
- cache
- system_param
- runtime_config
subdomain: grc
module: config
sensitivity: normal
name: aml.t_system_param运行时生效校验
aliases: []
related_services:
- svc_grc_component_connect_provider
related_tables:
- tbl_aml_t_system_param
related_scenarios:
- scn_grc_apollo_killswitch_restart_required
- scn_grc_rollback_path_selection
related_logs: []
related_requirements: []
related_failures: []
---

## 触发/入口
- 在 Basis Admin 的 Risk Param 页面修改 `aml.t_system_param` 的运行时配置（如标志位翻转）。
- 验证目标：新值是否在 `gp079_grc-component-connect-provider` 运行时真正生效。

## 前置条件
- 已具备 Basis Admin（`uat.intra.azure.test2pay.com/bigdata-admin/`）访问权限。
- 目标参数属于 `aml.t_system_param`（运行时生效类），而非 Apollo YAML（构建/重启时生效）。

## 操作步骤
1. 在 Risk Param 页面修改参数值并点 **Save**。
2. 进入 Basis → Function Query → **Cache Clear**。
3. 选择 `gp079_grc-component-connect-provider`。
4. 执行 `systemParam` Clear。
5. 同时执行 `ip` Clear（配套缓存）。
6. 触发一次 verifyRisk 请求以观察新值是否生效。

## DB 校验点
- `aml.t_system_param`：确认目标参数行的值已更新为期望值。
- 事件落库集合（`grc.t_payment_event_<yyyy>` 或 `grc.t_other_event_<yyyy>`）：通过 `riskStatus` 与 action outcome 字段比对新配置预期结果。

## 预期结果
- 仅点 Save 不足以让新值生效——必须完成 `systemParam` + `ip` 的 Cache Clear 后，运行时才会加载新值。
- 完成缓存清理后，后续 verifyRisk 请求按新参数执行规则，事件文档中的 `riskStatus` 与 action outcome 反映新配置。
- 若未清缓存即验证，结果仍为旧值，不能据此判断配置错误。
- 回滚同理：翻转 `aml.t_system_param` 标志位后必须清缓存才生效，按 blast radius 选择该路径 vs UI 禁用规则。
