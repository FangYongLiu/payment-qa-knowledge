---
id: domain_risk
object_type: Domain
name: risk
aliases: [风控/合规]
domain: risk
product: payment
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-06-24'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: [risk, 风控/合规]
related_services: [svc_acs, svc_voucher, svc_pfs_basis, svc_pfs_manager, svc_bigdata_admin, svc_bigdata_ws, svc_cps, svc_grc_check_identity_provider, svc_grc_component_connect_provider, svc_grc_cps_provider, svc_grc_engine_provider, svc_shortlink, svc_facepay_api, svc_calculator, svc_df_calculation, svc_fraud, svc_datasavvy, svc_crs]
---

# risk(风控/合规)

> 业务域总览(入口节点)。owner xinwei.cao,dewen.li。细节见各服务对象。

## 概述
风控与合规域:风控接入(acs)、GRC 身份/引擎(grc-*)、反欺诈(fraud)、风控基础(pfs-*)、黑名单计算(calculator/df-calculation)、facepay、crs 等。

## 覆盖范围
共 18 个服务:acs、voucher、pfs-basis、pfs-manager、bigdata-admin、bigdata-ws、cps、grc-check-identity-provider、grc-component-connect-provider、grc-cps-provider、grc-engine-provider、shortlink、facepay-api、calculator、df-calculation、fraud、datasavvy、crs。

## QA 关注点
- 待补。

## 流程 / 场景 / 排障 索引
本域 流程 / 场景 / 排障 / 自动化 对象索引:
- [[auto_basis_visual_rule_admin]](自动化:Basis 风控可视化规则管理后台)
- [[auto_dataeden_admin]](自动化:DataEden风控管理后台)
- [[flow_chargeback_processing]](流程:ChargeBack文件上传处理端到端流程)
- [[flow_verify_risk_request]](流程:verifyRisk请求处理端到端链路)
- [[scn_chargeback_mail_send_cases]](场景:ChargeBack邮件发送测试场景集)
- [[scn_grc_config_effectiveness]](场景:风控配置生效与回滚校验(双开关模型))
- [[scn_grc_event_routing_by_type]](场景:事件按类型路由到对应集合校验)
- [[scn_grc_geoip_log_not_reliable]](场景:GeoIP日志不可作为路径判定依据)
- [[scn_grc_identity_3ds_rule]](场景:风控核身规则配置控制3DS触发)
- [[scn_grc_ip_path_engagement_signature]](场景:通过remoteIpInfo._id判定IP解析路径)
- [[ts_risk_rule_not_firing]](排障:Visual Rule配置完成却不触发)
