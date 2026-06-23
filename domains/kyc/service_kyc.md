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
related_services: [svc_member, svc_outman, svc_acs, svc_pts]
related_tables: []
---

# kyc

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp078` · domain=`kyc`。

## 作用
实名认证（KYC，调 member）

## 系统中的位置
- 功能层:风控 / 合规 / KYC (Risk / Compliance / KYC)
- 业务域:`kyc`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_member]] member（会员 / 账户核心） · 188462 次 · high
- [[svc_outman]] outman · 11206 次 · high
- [[svc_acs]] acs（反欺诈 / 风控 + 渠道密钥） · 5046 次 · high
- [[svc_pts]] pts · 4 次 · high

**被调用(上游)—— 这些服务调用本服务:**
merchant-frontend

## 参与的业务场景(cgs 回归)
- §9. 登录 / KYC / 绑卡（basic_cases：`test_login` / `test_*eid*` / `test_bankcards`）
