---
id: svc_kyc
object_type: Service
domain: kyc
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp078
name: kyc
dev_owner: 沈纲领
aliases: [gp078_kyc]
related_services: [svc_member]
related_tables: []
---

# kyc

> 来源:UAT Kibana trace 观测(2026-06-22~23 UAT cgs 回归窗口,真实但非穷尽)+ 作用说明。候选待人审。app_group=`gp078` · domain=`kyc`。

## 作用
实名认证（KYC，调 member）

## 系统中的位置
- 功能层:风控 / 合规 / KYC (Risk / Compliance / KYC)
- 业务域:`kyc`

## 关联关系
**调用(下游)—— 本服务依赖这些服务完成处理:**
- [[svc_member]] member（会员 / 账户核心） · 26 次 · high

**被调用(上游)—— 这些服务调用本服务:**
merchant-frontend

## 参与的业务场景(cgs 回归)
- §9. 登录 / KYC / 绑卡（basic_cases：`test_login` / `test_*eid*` / `test_bankcards`）
