---
id: svc_personal
object_type: Service
domain: payment-tools
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp032
name: personal
dev_owner: Guoyou.Ma
aliases: [gp032_personal]
related_services: [svc_member, svc_acs, svc_pts, svc_fundout, svc_kyc, svc_cmf, svc_cashdesk_api]
related_tables: []
---

# personal

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp032` · domain=`payment-tools`。

## 作用
个人（C 端）账户服务 —— 登录 / 绑卡 / 转账 / 提现入口，调 member(Ma)/pts/acs/cmf

## 系统中的位置
- 功能层:会员 / 账户 / 卡 / 协议 (Member / Account / Card)
- 业务域:`payment-tools`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_member]] member（会员 / 账户核心） · 61829 次 · med·待核实
- [[svc_acs]] acs（反欺诈 / 风控 + 渠道密钥） · 41366 次 · high
- [[svc_pts]] pts · 30418 次 · high
- [[svc_fundout]] fundout（出款 / 代付核心） · 4868 次 · high
- [[svc_kyc]] kyc（实名认证） · 2993 次 · high
- [[svc_cmf]] cmf（渠道管理与资金） · 156 次 · high
- [[svc_cashdesk_api]] cashdesk-api（统一收银台） · 34 次 · high

## 涉及的 API / 数据库表
**暴露 / 相关 API:** [[api_personal_bind_customer]] 绑定客户接口 (bind-customer)、[[api_personal_v3_auth_login]] 客户登录接口(v3)

## 参与的业务场景(cgs 回归)
- §6. 提现（toC，`test_withdraw`）
- §9. 登录 / KYC / 绑卡（basic_cases：`test_login` / `test_*eid*` / `test_bankcards`）
- §10. 红包 / 社交支付、生活缴费、VAM（toC：`test_red_pkg` / `test_friend_transfer` / `test_vam` / 充值）
