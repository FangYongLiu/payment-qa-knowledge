---
id: svc_merchant_fundout
object_type: Service
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp083
name: merchant-fundout
subdomain: fundout
dev_owner: Sijia.Zhang
aliases: [gp083_merchant-fundout]
related_services: [svc_fundout, svc_merchant, svc_voucher, svc_tradeii, svc_ppcenter, svc_member, svc_cmf, svc_ues_ws, svc_pbs]
related_tables: []
related_scenarios: [scn_online_business_merchant_payout]
---

# merchant-fundout

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp083` · domain=`online-business`。

## 作用
商户出款 / 结算代付，调 merchant/fundout(Fos)/voucher/ppcenter

## 系统中的位置
- 功能层:出款 / 账务 / 对账 (Fundout / Accounting / Recon)
- 业务域:`online-business`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_fundout]] fundout（出款 / 代付核心） · 122987 次 · med·待核实
- [[svc_merchant]] merchant（商户主数据 / 商户管理） · 24591 次 · high
- [[svc_voucher]] voucher（全局 ID 与幂等凭证） · 11724 次 · high
- [[svc_tradeii]] tradeii（交易订单引擎） · 10422 次 · high
- [[svc_ppcenter]] ppcenter（产品中心） · 7797 次 · high
- [[svc_member]] member（会员 / 账户核心） · 3993 次 · high
- [[svc_cmf]] cmf（渠道管理与资金） · 3801 次 · high
- [[svc_ues_ws]] ues-ws（用户事件 / 数据服务） · 645 次 · med·待核实
- [[svc_pbs]] pbs（计费 / 定价） · 33 次 · high

## 涉及的 API / 数据库表
- **暴露/相关 API**:待补
- **读写的表**:待补

## 关键方法 / 入口
- 待补(本窗口未单独抽取 Dubbo/RPC 方法级)。

## 测试要点 / 排障 / 常见问题
- 待补(QA 视角:怎么测、已知坑、典型故障与定位)。

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp083` · domain=`online-business`。
