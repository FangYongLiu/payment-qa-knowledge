---
id: svc_member_front
object_type: Service
domain: wallet
status: active
owner: qianlong.wang
reviewer: qianlong.wang
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp135
name: member-front
dev_owner: 沈纲领
aliases: [gp135_member-front]
related_services: [svc_member, svc_kyc, svc_acs, svc_protocol, svc_gpoint, svc_holding, svc_voucher, svc_cashdesk_api, svc_ues_ws, svc_pts]
related_tables: []
---

# member-front

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp135` · domain=`wallet`。

## 作用
会员前置服务（member 的前置 / 聚合，调 acs）

## 系统中的位置
- 功能层:会员 / 账户 / 卡 / 协议 (Member / Account / Card)
- 业务域:`wallet`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_member]] member（会员 / 账户核心） · 107120 次 · high
- [[svc_kyc]] kyc（实名认证） · 28888 次 · high
- [[svc_acs]] acs（反欺诈 / 风控 + 渠道密钥） · 19494 次 · high
- [[svc_protocol]] protocol（代扣 / 签约协议管理） · 688 次 · high
- [[svc_gpoint]] gpoint · 526 次 · high
- [[svc_holding]] holding · 526 次 · high
- [[svc_voucher]] voucher（全局 ID 与幂等凭证） · 492 次 · high
- [[svc_cashdesk_api]] cashdesk-api（统一收银台） · 54 次 · high
- [[svc_ues_ws]] ues-ws（用户事件 / 数据服务） · 54 次 · med·待核实
- [[svc_pts]] pts · 46 次 · high

**被调用(上游)—— 这些服务调用本服务:**
cashierii

## 参与的业务场景(cgs 回归)
- §2. 收银台 / 收银（`test_bpg_paypage` 收银侧、cashier 用例）
- §9. 登录 / KYC / 绑卡（basic_cases：`test_login` / `test_*eid*` / `test_bankcards`）
