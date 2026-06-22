---
id: tbl_aml_t_system_param
object_type: Table
domain: risk-control
status: active
owner: consolidation
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-22'
source_type: consolidation
source_ref: consolidation:risk-control:b4
tags:
- 运行时配置
- 风控开关
- 缓存刷新
subdomain: grc
module: system-param
sensitivity: normal
name: AML系统参数表 t_system_param
aliases:
- aml.t_system_param
related_services:
- svc_grc_component_connect_provider
related_tables: []
related_scenarios:
- scn_grc_system_param_cache_refresh
- scn_grc_apollo_killswitch_restart_required
- scn_grc_rollback_path_selection
related_logs: []
related_requirements: []
related_failures: []
---

## 用途

`aml.t_system_param` 是 GRC 风控系统双开关模型中的**运行时配置层**，与 Apollo YAML（构建/重启时生效）相对，承担可在运行时通过缓存刷新生效的风控标志位配置。常用于回滚路径选择中，作为"翻转标志位 + 清缓存"的执行载体（与 UI 禁用规则二选一，按 blast radius 决定）。

## 关键列

原文未列出具体列结构；仅说明本表存储运行时生效的风控参数标志位（flag），由 GRC 组件 `gp079_grc-component-connect-provider` 加载使用。

## 主键/索引

原文未提供。

## 校验点(QA 关注)

- **生效方式**：本表是**运行时生效**，但并非自动热生效——仅在 Risk Param 页点 **Save 不足以让新值生效**，必须走缓存清理流程。
- **缓存刷新路径**：Basis → Function Query → Cache Clear → `gp079_grc-component-connect-provider` → `systemParam` Clear（IP 解析相关场景需同时执行 `ip` Clear）。
- **与 Apollo Kill Switch 的区分**：
  - Apollo YAML 为构建/重启时加载的 Kill Switch，**非热更新**，改完必须等 Tomcat 重启后再验证；
  - `aml.t_system_param` 走缓存刷新即可生效；
  - 验证前需先确认改的是哪一层，避免在未重启 / 未清缓存时立即下结论。
- **回滚路径选择**：翻转 `aml.t_system_param` 标志位 + 清缓存 vs UI 禁用规则，按影响范围（blast radius）选择，QA 需明确本次回滚走的是哪一条。
- **联动 IP 解析**：当涉及 IP-area 解析新旧路径切换时，除 `systemParam` Clear 外还要 `ip` Clear，路径是否真正切换以事件文档 `remoteIpInfo._id` 形态为准，不要以 `GeoIPOperaUtil` 日志为准（该日志仅在出错时打）。
