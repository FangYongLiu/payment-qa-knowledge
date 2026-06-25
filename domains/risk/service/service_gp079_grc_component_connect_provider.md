---
id: svc_grc_component_connect_provider
object_type: Service
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp079
name: grc-component-connect-provider
dev_owner: Dewen.Li
aliases: [gp079_grc-component-connect-provider]
related_services: []
related_tables: []
---

# grc-component-connect-provider

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp079` · domain=`risk`。

## 作用
(本窗口未观测到该服务的运行时活动,作用待业务补充。)

## 系统中的位置
- 业务域:`risk`

## 关联关系
(本窗口未观测到与其它服务的调用关系)

## 涉及的 API / 数据库表
- **暴露/相关 API**:待补
- **读写的表**:待补

## 关键方法 / 入口
- 待补(本窗口未单独抽取 Dubbo/RPC 方法级)。

## 测试要点 / 排障 / 常见问题
- 待补(QA 视角:怎么测、已知坑、典型故障与定位)。

## 相关流程 / 场景 / 排障(反向)
本服务涉及的流程/场景/排障(由对方 `related_services` 指向,反向汇总):
- [[auto_basis_visual_rule_admin]](自动化:Basis 风控可视化规则管理后台)
- [[flow_botim_transfer]](流程:BOTIM/ToC 转账与加款端到端流程)
- [[flow_verify_risk_request]](流程:verifyRisk请求处理端到端链路)
- [[scn_grc_config_effectiveness]](场景:风控配置生效与回滚校验(双开关模型))
- [[scn_grc_event_routing_by_type]](场景:事件按类型路由到对应集合校验)
- [[scn_grc_geoip_log_not_reliable]](场景:GeoIP日志不可作为路径判定依据)
- [[scn_grc_ip_path_engagement_signature]](场景:通过remoteIpInfo._id判定IP解析路径)
- [[ts_risk_rule_not_firing]](排障:Visual Rule配置完成却不触发)

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp079` · domain=`risk`。
