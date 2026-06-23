---
id: svc_ppcenter
object_type: Service
domain: payment-tools
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp047
name: ppcenter
dev_owner: 黄美美
aliases: [gp047_ppcenter]
related_services: []
related_tables: []
---

# ppcenter

> 来源:UAT Kibana trace 观测(2026-06-22~23 UAT cgs 回归窗口,真实但非穷尽)+ 作用说明。候选待人审。app_group=`gp047` · domain=`payment-tools`。

## 作用
产品中心（商户开通产品状态 queryMerchantOpenedProductStatus，被 acquire/device/merchant-fundout 调用）

## 系统中的位置
- 功能层:营销 / 产品 / 报价 (Marketing / Product / Quote)
- 业务域:`payment-tools`

## 关联关系

**被调用(上游)—— 这些服务调用本服务:**
device, acquireii, merchant-fundout

## 参与的业务场景(cgs 回归)
- §1. 直连支付 / 预授权 / DCC（toB，`test_direct_pay` / `test_pre_auth_capture` / `test_bpg_paypage`）

## 观测到的对外方法
queryMerchantOpenedProductStatus
