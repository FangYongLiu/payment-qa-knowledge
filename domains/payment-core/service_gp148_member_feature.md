---
id: svc_member_feature
object_type: Service
domain: payment-core
status: active
owner: qianlong.wang
reviewer: qianlong.wang
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp148
name: member-feature
dev_owner: Gangling.Shen
aliases: [gp148_member-feature]
related_services: [svc_member, svc_acs, svc_member_front, svc_grc_check_identity_provider]
related_tables: []
---

# member-feature

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp148` · domain=`wallet`。

## 作用
会员 / 账户服务（feature）  **(据名推断 · 待核实:无作用文字证据,但下方有观测到的调用关系)**

## 系统中的位置
- 业务域:`wallet`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_member]] member（会员 / 账户核心） · 750 次 · high
- [[svc_acs]] acs（反欺诈 / 风控 + 渠道密钥） · 18 次 · high
- [[svc_member_front]] member-front（会员前置服务） · 6 次 · high
- [[svc_grc_check_identity_provider]] grc-check-identity-provider（风控合规身份校验） · 4 次 · med·待核实
