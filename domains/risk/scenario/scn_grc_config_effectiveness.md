---
id: scn_grc_config_effectiveness
object_type: Scenario
name: 风控配置生效与回滚校验(双开关模型)
aliases: []
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:AQ/2161541121
tags:
- apollo
- killswitch
- system_param
- cache
- rollback
related_services:
- svc_grc_component_connect_provider
related_tables:
- tbl_aml_t_system_param
---

# 风控配置生效与回滚校验(双开关模型)

## 触发/入口
修改了 GRC 风控配置(Apollo YAML Kill Switch 类,或 `aml.t_system_param` 运行时类),需要验证新值是否生效;或风控规则上线后需回滚。适用组件:[[svc_grc_component_connect_provider]]。

## 关联关系
- **涉及服务**:[[svc_grc_component_connect_provider]](= `related_services`)
- **校验的表**:[[tbl_aml_t_system_param]](= `related_tables`)
- **缓存清理入口**:Basis Admin([[auto_basis_visual_rule_admin]]),GENERAL → Function Query → Cache Clear

## 前置条件
- 已识别待验证/待回滚的配置项,并确认它落在双开关模型的哪一层:
  - **Apollo YAML**:构建期或 Tomcat 重启时加载,Kill Switch 类配置走此路径,**非热更新**。
  - **`aml.t_system_param`**([[tbl_aml_t_system_param]]):运行时配置,可通过缓存刷新生效。
- 已具备 Basis Admin(`uat.intra.azure.test2pay.com/bigdata-admin/`)访问权限。

## 操作步骤
### A. Apollo YAML / Kill Switch(非热更新)
1. 在 Apollo 中修改目标 Kill Switch 配置项并发布。
2. 触发 `gp079_grc-component-connect-provider` 所在 Tomcat 重启,等待服务完成启动加载新 YAML。
3. 重启完成后再发起 verifyRisk 验证。**不要在重启前**根据请求结果对是否生效下结论。

### B. aml.t_system_param(运行时,缓存刷新)
1. 在 Risk Param 页修改参数值并点 **Save**(仅 Save 不足以生效)。
2. Basis → Function Query → **Cache Clear** → 选择 `gp079_grc-component-connect-provider`。
3. 执行 `systemParam` Clear,并配套执行 `ip` Clear。
4. 触发一次 verifyRisk 观察新值是否生效。

### C. 回滚路径选择(按 blast radius,从小到大)
1. **Visual Rule UI 直接 disable 单条规则**——最小范围。
2. **翻转 `aml.t_system_param` 标志位 + 清缓存**(`systemParam` + `ip`)——影响该参数控制的整段逻辑。
3. **Kill Switch + Tomcat 重启**——最大范围,影响整个 GRC 组件层。

## DB 校验点
- `aml.t_system_param`:确认目标参数/标志位已更新为期望值。
- 事件落库集合(`grc.t_payment_event_<yyyy>` / `grc.t_other_event_<yyyy>`):通过 `riskStatus` 与 action outcome 比对新配置预期。

## 预期结果
- 运行时参数:**仅 Save 不生效**,完成 `systemParam` + `ip` Cache Clear 后才加载新值;未清缓存即验证会拿到旧值,不能据此判断配置错误。
- 另有规则发布侧约 **35s** 缓存重载窗口:规则 ENABLED 后需等该窗口才真正 live。
- Apollo Kill Switch:Tomcat 重启后新值才生效,重启前的行为不能作为生效判据。
- 回滚:按 blast radius 选择路径,翻转 `aml.t_system_param` 后必须清缓存才生效。
- 排错切入点:改完没生效先确认是否走过 Cache Clear(而非只点 Save);规则有日志但无动作检查是否仍 Trial 模式;Kill Switch 改完立即无效检查 Tomcat 是否已重启。详见 [[ts_risk_rule_not_firing]]。
