---
id: svc_deposit
object_type: Service
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp011
name: deposit
aliases: [gp011_deposit]
related_services: [svc_cashierii, svc_tradeii, svc_acs]
related_tables: []
---

# deposit

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp011` · domain=`service-catalog`。

## 作用
充值 / 存款服务（被 escrow/vis 调用，推断）  **(待核实:仅凭调用关系推断)**

## 系统中的位置
- 功能层:会员 / 账户 / 卡 / 协议 (Member / Account / Card)
- 业务域:`service-catalog`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_cashierii]] cashierii（收银核心） · 405 次 · high
- [[svc_tradeii]] tradeii（交易订单引擎） · 405 次 · high
- [[svc_acs]] acs（反欺诈 / 风控 + 渠道密钥） · 102 次 · high

**被调用(上游)—— 这些服务调用本服务:**
escrow, vis

## 涉及的 API / 数据库表
**暴露 / 相关 API:** [[api_payby_notify_vam_deposit]] VAM充值通知接口

## 参与的业务场景(cgs 回归)
- §10. 红包 / 社交支付、生活缴费、VAM（toC：`test_red_pkg` / `test_friend_transfer` / `test_vam` / 充值）
