---
id: svc_npss
object_type: Service
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp222
name: npss
dev_owner: Qian.Wang
aliases: [gp222_npss]
related_services: [svc_member, svc_voucher, svc_tradeii, svc_grc_check_identity_provider, svc_pns, svc_reconciliation, svc_npss_gateway, svc_vis, svc_visii, svc_cmf]
related_tables: []
---

# npss

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp222` · domain=`service-catalog`。

## 作用
即时支付 / 账单（NPSS，被 rtp 调用）

## 系统中的位置
- 功能层:即时支付 / 账单 (NPSS / Bill / RTP)
- 业务域:`service-catalog`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_member]] member（会员 / 账户核心） · 239632 次 · high
- [[svc_voucher]] voucher（全局 ID 与幂等凭证） · 51212 次 · high
- [[svc_tradeii]] tradeii（交易订单引擎） · 50047 次 · high
- [[svc_grc_check_identity_provider]] grc-check-identity-provider（风控合规身份校验） · 46818 次 · med·待核实
- [[svc_pns]] pns（支付通知服务） · 41246 次 · high
- [[svc_reconciliation]] reconciliation（对账） · 20707 次 · high
- [[svc_npss_gateway]] npss-gateway（NPSS） · 17670 次 · high
- [[svc_vis]] vis · 3871 次 · high
- [[svc_visii]] visii · 1638 次 · high
- [[svc_cmf]] cmf（渠道管理与资金） · 28 次 · high

**被调用(上游)—— 这些服务调用本服务:**
rtp, npss-gateway

## 参与的业务场景(cgs 回归)
- §8. 账单 / 即时支付（`test_ppcTransaction`，NPSS）
