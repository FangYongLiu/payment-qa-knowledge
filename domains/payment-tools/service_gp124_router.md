---
id: svc_router
object_type: Service
domain: payment-tools
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp124
name: router
dev_owner: 张鹤飞
aliases: [gp124_router]
related_services: [svc_onboarding, svc_cmf]
related_tables: []
---

# router

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp124` · domain=`payment-tools`。

## 作用
渠道路由（Channel Router）—— 按 apiType 选可用渠道（queryChannelArchive/getChannelsByApiTypes），下游 onboarding/cmf

## 系统中的位置
- 功能层:交易 / 支付中台 (Trade / Payment Core)
- 业务域:`payment-tools`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_onboarding]] onboarding（商户 / 用户入网） · 497702 次 · high
- [[svc_cmf]] cmf（渠道管理与资金） · 36844 次 · high

**被调用(上游)—— 这些服务调用本服务:**
remittance, cmf, cmf-task, reconciliation, cregister

## 涉及的 API / 数据库表
**读写的表:** [[tbl_router_t_channel_result_code]] 渠道返回码映射表 t_channel_result_code

## 参与的业务场景(cgs 回归)
- §1. 直连支付 / 预授权 / DCC（toB，`test_direct_pay` / `test_pre_auth_capture` / `test_bpg_paypage`）
- §4. 卡渠道入金 3DS（`test_mpgs_fundIn` / `test_cko_fundIn`）
- §5. 银行/卡转账、出款（`test_transfer_to_bank` / `test_transfer_to_card`）
- §7. 跨境汇款（toC，`test_remittance`）
- §9. 登录 / KYC / 绑卡（basic_cases：`test_login` / `test_*eid*` / `test_bankcards`）
