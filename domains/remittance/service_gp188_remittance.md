---
id: svc_remittance
object_type: Service
domain: remittance
status: active
owner: lei.pan
reviewer: lei.pan
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp188
name: remittance
dev_owner: 喻赛
aliases: [gp188_remittance]
related_services: [svc_member, svc_router, svc_acs, svc_cms, svc_grc_check_identity_provider, svc_paylater, svc_tradeii, svc_voucher, svc_pns, svc_reconciliation, svc_query, svc_aml, svc_protocol, svc_ufs2]
related_tables: []
---

# remittance

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp188` · domain=`remittance`。

## 作用
跨境汇款核心 —— 编排 member/router/acs/tradeii/reconciliation + 各汇款渠道（terrapay/arp/fuze）

## 系统中的位置
- 功能层:汇款 (Remittance)
- 业务域:`remittance`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_member]] member（会员 / 账户核心） · 5703405 次 · high
- [[svc_router]] router（渠道路由） · 4379425 次 · high
- [[svc_acs]] acs（反欺诈 / 风控 + 渠道密钥） · 41081 次 · high
- [[svc_cms]] cms（内容 / 配置管理） · 20629 次 · high
- [[svc_grc_check_identity_provider]] grc-check-identity-provider（风控合规身份校验） · 15935 次 · med·待核实
- [[svc_paylater]] paylater · 7718 次 · high
- [[svc_tradeii]] tradeii（交易订单引擎） · 6862 次 · high
- [[svc_voucher]] voucher（全局 ID 与幂等凭证） · 5007 次 · high
- [[svc_pns]] pns（支付通知服务） · 1940 次 · high
- [[svc_reconciliation]] reconciliation（对账） · 1820 次 · high
- [[svc_query]] query（查询 / 报表服务） · 1724 次 · high
- [[svc_aml]] aml（反洗钱） · 613 次 · high
- [[svc_protocol]] protocol（代扣 / 签约协议管理） · 205 次 · high
- [[svc_ufs2]] ufs2（用户文件 / 数据服务） · 181 次 · med·待核实

**被调用(上游)—— 这些服务调用本服务:**
fcw

## 参与的业务场景(cgs 回归)
- §7. 跨境汇款（toC，`test_remittance`）
