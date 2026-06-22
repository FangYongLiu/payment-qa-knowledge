---
id: scn_grc_apollo_killswitch_restart_required
object_type: Scenario
domain: risk-control
status: active
owner: consolidation
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-22'
source_type: consolidation
source_ref: consolidation:risk-control:b4
tags:
- apollo
- killswitch
- restart
- non-hot-reload
subdomain: grc
module: config
sensitivity: normal
name: Apollo Kill Switch非热更新校验
aliases: []
related_services:
- svc_grc_component_connect_provider
related_tables: []
related_scenarios:
- scn_grc_system_param_cache_refresh
- scn_grc_rollback_path_selection
related_logs: []
related_requirements: []
related_failures: []
---

## 触发/入口
- 修改了 GRC 风控的 Apollo YAML 配置（Kill Switch 类配置），需要验证新值是否已生效。
- 适用组件：`gp079_grc-component-connect-provider`。

## 前置条件
- 待验证开关属于 **Apollo YAML** 一层（非 `aml.t_system_param`）。
- Apollo YAML 配置在构建期或 Tomcat 重启时加载，**非热更新**。
- 已知另一类运行时开关 `aml.t_system_param` 走缓存刷新路径，不适用本场景。

## 操作步骤
1. 在 Apollo 中修改目标 Kill Switch 配置项并发布。
2. 触发 `gp079_grc-component-connect-provider` 所在 Tomcat 重启（构建/重启动作）。
3. 等待服务完成启动加载新 YAML。
4. 重启完成后，再发起 verifyRisk 请求进行验证。
5. **不要在重启前**根据请求结果对 Kill Switch 是否生效下结论。

## DB 校验点
- 本场景属于配置生效校验，不涉及特定 DB 表落库校验。
- 与之对照：`aml.t_system_param` 类开关需通过 Basis → Function Query → Cache Clear → `gp079_grc-component-connect-provider` → `systemParam` Clear 刷新缓存生效，不属于本场景。

## 预期结果
- Tomcat 重启后，Apollo YAML 中新的 Kill Switch 值被加载并生效。
- 重启之前观察到的 verifyRisk 行为不能作为 Kill Switch 已生效/未生效的判定依据。
- 回滚路径选择时，Apollo Kill Switch 翻转需重启成本，应与 UI 禁用规则、`aml.t_system_param` 翻转+清缓存按 blast radius 权衡。
