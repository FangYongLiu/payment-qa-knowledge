---
id: svc_personal
object_type: Service
domain: wallet
status: active
owner: qianlong.wang
reviewer: qianlong.wang
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp032
name: personal
dev_owner: 刘智斌
aliases: [gp032_personal]
related_services: [svc_member, svc_pts, svc_fundout, svc_acs, svc_cmf]
related_tables: []
---

# personal

> 来源:UAT Kibana trace 观测(2026-06-22~23 UAT cgs 回归窗口,真实但非穷尽)+ 作用说明。候选待人审。app_group=`gp032` · domain=`wallet`。

## 作用
个人（C 端）账户服务 —— 登录 / 绑卡 / 转账 / 提现入口，调 member(Ma)/pts/acs/cmf

## 系统中的位置
- 功能层:会员 / 账户 / 卡 / 协议 (Member / Account / Card)
- 业务域:`wallet`

## 关联关系
**调用(下游)—— 本服务依赖这些服务完成处理:**
- [[svc_member]] member（会员 / 账户核心） · 344 次 · med·待核实
- [[svc_pts]] pts · 156 次 · high
- [[svc_fundout]] fundout（出款 / 代付核心） · 72 次 · high
- [[svc_acs]] acs（反欺诈 / 风控 + 渠道密钥） · 70 次 · high
- [[svc_cmf]] cmf（渠道管理与资金） · 4 次 · high

## 参与的业务场景(cgs 回归)
- §6. 提现（toC，`test_withdraw`）
- §9. 登录 / KYC / 绑卡（basic_cases：`test_login` / `test_*eid*` / `test_bankcards`）
- §10. 红包 / 社交支付、生活缴费、VAM（toC：`test_red_pkg` / `test_friend_transfer` / `test_vam` / 充值）
