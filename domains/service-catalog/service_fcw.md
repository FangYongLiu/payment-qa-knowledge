---
id: svc_fcw
object_type: Service
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp039
name: fcw
aliases: [gp039_fcw]
related_services: [svc_cmf, svc_remittance]
related_tables: []
---

# fcw

> 来源:UAT Kibana trace 观测(2026-06-22~23 UAT cgs 回归窗口,真实但非穷尽)+ 作用说明。候选待人审。app_group=`gp039` · domain=`service-catalog`。

## 作用
前置渠道网关（Front Channel Web）—— 3DS 跳转 / 渠道通知页；下游 cmf/remittance

## 系统中的位置
- 功能层:接入网关 / 前端 BFF (Gateway / Frontend)
- 业务域:`service-catalog`

## 关联关系
**调用(下游)—— 本服务依赖这些服务完成处理:**
- [[svc_cmf]] cmf（渠道管理与资金） · 364 次 · high
- [[svc_remittance]] remittance（跨境汇款核心） · 36 次 · high

## 参与的业务场景(cgs 回归)
- §1. 直连支付 / 预授权 / DCC（toB，`test_direct_pay` / `test_pre_auth_capture` / `test_bpg_paypage`）
- §4. 卡渠道入金 3DS（`test_mpgs_fundIn` / `test_cko_fundIn`）
