---
id: svc_onboarding
object_type: Service
domain: portal-operations
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp254
name: onboarding
aliases: [gp254_onboarding]
related_services: [svc_vis]
related_tables: []
---

# onboarding

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp254` · domain=`portal-operations`。

## 作用
商户 / 用户入网（被 router/qpay-mpgs 调用，加载商户 MerchantFacade）

## 系统中的位置
- 功能层:会员 / 账户 / 卡 / 协议 (Member / Account / Card)
- 业务域:`portal-operations`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_vis]] vis · 105 次 · high

**被调用(上游)—— 这些服务调用本服务:**
router, qpay-mpgs

## 参与的业务场景(cgs 回归)
- §4. 卡渠道入金 3DS（`test_mpgs_fundIn` / `test_cko_fundIn`）
- §9. 登录 / KYC / 绑卡（basic_cases：`test_login` / `test_*eid*` / `test_bankcards`）
