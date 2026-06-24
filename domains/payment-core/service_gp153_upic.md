---
id: svc_upic
object_type: Service
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp153
name: upic
dev_owner: Yu.Tang
aliases: [gp153_upic]
related_services: [svc_cms, svc_member, svc_pcs, svc_grc_check_identity_provider, svc_protocol]
related_tables: []
---

# upic

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp153` · domain=`payment-core`。

## 作用
upic  **(据名推断 · 待核实:无作用文字证据,但下方有观测到的调用关系)**

## 系统中的位置
- 业务域:`payment-core`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_cms]] cms（内容 / 配置管理） · 3766 次 · high
- [[svc_member]] member（会员 / 账户核心） · 1732 次 · high
- [[svc_pcs]] pcs · 56 次 · high
- [[svc_grc_check_identity_provider]] grc-check-identity-provider（风控合规身份校验） · 42 次 · med·待核实
- [[svc_protocol]] protocol（代扣 / 签约协议管理） · 18 次 · high

## 涉及的 API / 数据库表
- **暴露/相关 API**:待补
- **读写的表**:待补

## 关键方法 / 入口
- 待补(本窗口未单独抽取 Dubbo/RPC 方法级)。

## 测试要点 / 排障 / 常见问题

**UAT Kibana 7d 错误观测**(自动回归 + UAT 流量,app_id=`upic`):
- ERROR 2122 次,主要:`CardEnrollmentRequester`×1002、`CardEnrollmentEventHandler`×892
- WARN 15 次(均为基础设施噪声)
- ⚠️ 频次可能含 UAT 测试数据噪声,**真坑 vs 噪声需人工确认**;高频项见域级排障对象。
- 更多 QA 校验点(怎么测 / 已知坑 / 典型故障定位)待补。
## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp153` · domain=`payment-core`。
