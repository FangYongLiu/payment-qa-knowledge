---
id: svc_ppcenter
object_type: Service
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp047
name: ppcenter
dev_owner: Yadong.Lu
aliases: [gp047_ppcenter]
related_services: [svc_member, svc_acs, svc_contract]
related_tables: []
---

# ppcenter

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp047` · domain=`payment-tools`。

## 作用
产品中心（商户开通产品状态 queryMerchantOpenedProductStatus，被 acquire/device/merchant-fundout 调用）

## 系统中的位置
- 功能层:营销 / 产品 / 报价 (Marketing / Product / Quote)
- 业务域:`payment-tools`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_member]] member（会员 / 账户核心） · 1820 次 · high
- [[svc_acs]] acs（反欺诈 / 风控 + 渠道密钥） · 102 次 · high
- [[svc_contract]] contract · 14 次 · high

**被调用(上游)—— 这些服务调用本服务:**
device, acquireii, merchant-fundout

## 参与的业务场景(cgs 回归)
- §1. 直连支付 / 预授权 / DCC（toB，`test_direct_pay` / `test_pre_auth_capture` / `test_bpg_paypage`）

## 观测到的对外方法
queryMerchantOpenedProductStatus
