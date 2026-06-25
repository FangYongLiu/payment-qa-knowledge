---
id: ts_risk_rule_not_firing
object_type: Troubleshooting
name: Visual Rule配置完成却不触发
aliases: []
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:AQ/2161541121
tags:
- visual-rule
- not-firing
- troubleshooting
related_services:
- svc_grc_component_connect_provider
related_tables:
- tbl_grc_t_payment_event
- tbl_grc_t_other_event
- tbl_aml_t_system_param
---

# Visual Rule配置完成却不触发

## 症状
一条 Visual Rule 看似配置完成,却没有在 verifyRisk 事件中触发(无命中、无 action、list repo 无写入)。

## 关联关系
- **涉及服务**:[[svc_grc_component_connect_provider]](= `related_services`)
- **涉及表**:[[tbl_grc_t_payment_event]]、[[tbl_grc_t_other_event]]、[[tbl_aml_t_system_param]](= `related_tables`)
- **相关接口/场景**:[[api_grc_verify_risk]]、[[scn_grc_config_effectiveness]]、[[scn_grc_ip_path_engagement_signature]]
- **管理后台**:[[auto_basis_visual_rule_admin]]

## 可能根因(按出现频率从高到低)
- **Checkpoint 不匹配**:规则挂载的 checkpoint 与事件实际进入的 checkpoint 不一致;确认 checkpoint 是否绑定到真实 CGS 事件源(而非 test-only)。
- **策略版本未部署**:一个 Strategy 同时只有 ONE version 处于 deployed;挂在非 deployed 版本下的规则在真实事件上永远不会 fire。
- **规则状态未到 ENABLED**:仍处于 `DRAFT` 或 `TRIAL`;TRIAL 仅写日志不执行 action,rule-level 与 strategy-level 短路各自独立。
- **缓存陈旧**:审批通过后需等 ~35s 缓存重载;`aml.t_system_param` 改动后必须走 Cache Clear,仅 "Risk Param → Save" 不够。
- **字段名大小写/拼写不一致**:payload 字段必须与 list repo 列字段名完全一致(case-sensitive,无 auto-mapping)。
- **Kill Switch 未生效**:Apollo YAML 类 Kill Switch 非热加载,需 Tomcat 重启后再验证。
- **List repo 列形态选错**:`oneRow` 部分空值静默跳过该 attr,`mostRow` 部分空值 abort 整行。
- **repoNo 异常**:未在 `bigdata_system_dic.addListRepos` 字典内的 repoNo 被拒绝;目标 list repo 已被热删除时 graceful no-op + 一行日志,不抛异常。

## 排查步骤
1. **确认规则状态**:Visual Rule UI 检查是否 `ENABLED`;AstraShield Audit Record 确认审批已通过。
2. **确认策略版本**:Strategy Manager 查看当前 deployed 版本号,确认规则挂在该版本下。
3. **确认 checkpoint 绑定**:核对 checkpoint 名称(如 `FT_ATL_CP`)及其对接的事件源。
4. **执行缓存清理**:Basis → Function Query → Cache Clear → `gp079_grc-component-connect-provider` → `systemParam` Clear + `ip` Clear(见 [[scn_grc_config_effectiveness]])。
5. **核对字段名**:对照 list repo `fieldDef`(mostRow)或 `listRepoFieldType`(oneRow),逐字段比对 payload key(含大小写)。
6. **查 Kibana 日志**:用 `eventId` / `cisTicket` / `orderNo` 检索 GRC 服务日志,定位规则是否命中、是否走 trial 短路。注意 `GeoIPOperaUtil` 仅在出错时打日志。
7. **查 DB 落库**:
   - List repo:`db.bigdata_list_repo_data.find({repoNo:'<target>'}).sort({_id:-1}).limit(3)`
   - 事件文档:`t_payment_event_<yyyy>` / `t_other_event_<yyyy>` 查 `riskStatus`、`remoteIpInfo`、`trueIpInfo` 与 action 结果。
8. **核对 Audit memo**:格式应为 `'from visual rule, eventId=<id>'`,其中 `eventId` 取自请求 Header 而非 body。

## 处理/规避
- 大多数问题可在上述清单内定位。路径判定问题以事件文档 `remoteIpInfo._id` 形态为准(见 [[scn_grc_geoip_log_not_reliable]])。
- 仍无法定位时按问题域升级联系人:
  - Risk Dev(引擎/代码层):chao.li@astratech.ae、Abhimanyu.Singh@astratech.ae
  - BMOC(商户配置):通过 BMOC Portal 对接业务侧
  - Infra/Ops(缓存、Apollo、VPN、账号):zhiqi.jin@astratech.ae
  - QA(用例与验证流程):ext_Nitesh.Parasher@astratech.ae
