---
id: svc_deposit
object_type: Service
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp011
name: deposit
dev_owner: Qian.Wang,Yu.Tang
aliases: [gp011_deposit]
related_services: [svc_cashierii, svc_tradeii, svc_acs]
related_tables: []
---

# deposit

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp011` · domain=`payment-core`。

## 作用
充值 / 存款服务（被 escrow/vis 调用，推断）  **(待核实:仅凭调用关系推断)**

## 系统中的位置
- 功能层:会员 / 账户 / 卡 / 协议 (Member / Account / Card)
- 业务域:`payment-core`

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

## 关键方法 / 入口
- 待补(本窗口未单独抽取 Dubbo/RPC 方法级)。

## 测试要点 / 排障 / 常见问题
- 待补(QA 视角:怎么测、已知坑、典型故障与定位)。

## 相关流程 / 场景 / 排障(反向)
本服务涉及的流程/场景/排障(由对方 `related_services` 指向,反向汇总):
- [[scn_wallet_vam_iban_apply_activate]](场景:VAM IBAN 虚拟账户申请激活与交易通知 (VAM IBAN Apply / Activate / Notify))

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp011` · domain=`payment-core`。
