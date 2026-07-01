---
id: svc_ppc
object_type: Service
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp212
name: ppc
dev_owner: Yu.Tang
aliases: [gp212_ppc]
related_services: [svc_member, svc_voucher, svc_dpm_manager, svc_grc_check_identity_provider, svc_pfs_payment, svc_reconciliation, svc_pns, svc_csimple, svc_cms, svc_shortlink, svc_merchant, svc_tradeii, svc_query, svc_crs]
related_tables: []
---

# ppc

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp212` · domain=`payment-core`。

## 作用
ppc  **(据名推断 · 待核实:无作用文字证据,但下方有观测到的调用关系)**

## 系统中的位置
- 业务域:`payment-core`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_member]] member（会员 / 账户核心） · 47501 次 · high
- [[svc_voucher]] voucher（全局 ID 与幂等凭证） · 35799 次 · high
- [[svc_dpm_manager]] dpm-manager（账务平台管理） · 5258 次 · high
- [[svc_grc_check_identity_provider]] grc-check-identity-provider（风控合规身份校验） · 1360 次 · med·待核实
- [[svc_pfs_payment]] pfs-payment（支付履约 / 清分） · 1160 次 · high
- [[svc_reconciliation]] reconciliation（对账） · 832 次 · high
- [[svc_pns]] pns（支付通知服务） · 754 次 · high
- [[svc_csimple]] csimple · 241 次 · high
- [[svc_cms]] cms（内容 / 配置管理） · 109 次 · high
- [[svc_shortlink]] shortlink · 77 次 · high
- [[svc_merchant]] merchant（商户主数据 / 商户管理） · 40 次 · high
- [[svc_tradeii]] tradeii（交易订单引擎） · 38 次 · high
- [[svc_query]] query（查询 / 报表服务） · 3 次 · high
- [[svc_crs]] crs · 1 次 · high

## 涉及的 API / 数据库表
**暴露 / 相关 API:** [[api_ppc_jeebly_delivery_status]] Jeebly配送状态回调接口、[[api_ppc_card_apply_virtual]] 申请虚拟卡接口、[[api_ppc_card_set_pin]] 设置卡PIN接口、[[api_ppc_card_lock]] 锁卡接口、[[api_ppc_card_reset_pin]] 重置卡PIN接口、[[api_ppc_card_apply_physical]] 申请实体卡接口、[[api_ppc_card_replace]] 替换卡接口、[[api_ppc_yse_clearing_notify]] YSE清算回调接口、[[api_ppc_card_close]] 关闭卡接口、[[api_ppc_card_unlock]] 解锁卡接口、[[api_ppc_card_activate]] 激活实体卡接口、[[api_ppc_yse_auth_notify]] YSE授权回调接口、[[api_ppc_card_track_physical]] 跟踪实体卡配送接口

## 参与的业务场景(cgs 回归)
- §1. 直连支付 / 预授权 / DCC（toB，`test_direct_pay` / `test_pre_auth_capture` / `test_bpg_paypage`）

## 关键方法 / 入口
- 待补(本窗口未单独抽取 Dubbo/RPC 方法级)。

## 测试要点 / 排障 / 常见问题
- 待补(QA 视角:怎么测、已知坑、典型故障与定位)。

## 相关流程 / 场景 / 排障(反向)
本服务涉及的流程/场景/排障(由对方 `related_services` 指向,反向汇总):
- [[flow_jaywan_prepaid_card]](流程:Jaywan 预付卡端到端流程(Dgpay 渠道))
- [[flow_ppc_card_lifecycle]](流程:PPC 卡端到端业务流程(开卡→激活→交易→清算→关卡))
- [[flow_wps_company_onboarding_to_payroll]](流程:WPS 企业入驻到发薪端到端流程)
- [[scn_card_lifecycle_transitions]](场景:PPC 卡生命周期状态转换测试场景集)

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp212` · domain=`payment-core`。
