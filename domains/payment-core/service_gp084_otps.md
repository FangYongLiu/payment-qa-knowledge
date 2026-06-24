---
id: svc_otps
object_type: Service
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp084
name: otps
dev_owner: Yadong.Lu
aliases: [gp084_otps]
related_services: [svc_member, svc_acs]
related_tables: []
---

# otps

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp084` · domain=`payment-core`。

## 作用
otps  **(据名推断 · 待核实:无作用文字证据,但下方有观测到的调用关系)**

## 系统中的位置
- 业务域:`payment-core`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_member]] member（会员 / 账户核心） · 5520 次 · med·待核实
- [[svc_acs]] acs（反欺诈 / 风控 + 渠道密钥） · 5514 次 · high
