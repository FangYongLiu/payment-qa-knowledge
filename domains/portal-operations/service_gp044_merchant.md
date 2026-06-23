---
id: svc_merchant
object_type: Service
domain: portal-operations
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp044
name: merchant
aliases: [gp044_merchant]
related_services: [svc_aml, svc_authorization_service, svc_statementii]
related_tables: []
---

# merchant

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp044` · domain=`portal-operations`。

## 作用
商户主数据 / 商户管理（queryStaffPage/getStaff、ProductAudit、Aml）—— 被收单 / 收银 / 出款调用

## 系统中的位置
- 功能层:即时支付 / 账单 (NPSS / Bill / RTP)
- 业务域:`portal-operations`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_aml]] aml（反洗钱） · 1233947 次 · high
- [[svc_authorization_service]] authorization-service（授权服务） · 4090 次 · med·待核实
- [[svc_statementii]] statementii（账单 / 对账单） · 45 次 · high

**被调用(上游)—— 这些服务调用本服务:**
merchant-frontend, merchant-fundout, cashierii, mssii, fundout, device

## 涉及的 API / 数据库表
**暴露 / 相关 API:** [[api_merchant_bizopen_wps]] 商户开通WPS接口、[[api_merchant_apply_add]] 商户申请新增接口
**读写的表:** [[tbl_merchant_device]] 商户设备关系表、[[tbl_merchant_webhook_config]] 商户Webhook配置表、[[tbl_merchant_db]] 商户库(merchant)核心表

## 参与的业务场景(cgs 回归)
- §1. 直连支付 / 预授权 / DCC（toB，`test_direct_pay` / `test_pre_auth_capture` / `test_bpg_paypage`）
- §2. 收银台 / 收银（`test_bpg_paypage` 收银侧、cashier 用例）
- §5. 银行/卡转账、出款（`test_transfer_to_bank` / `test_transfer_to_card`）

## 观测到的对外方法
queryStaffPage, getStaff
