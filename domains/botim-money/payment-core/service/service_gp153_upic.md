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
- **暴露 API**(Dubbo,来源 `upic-dubbo-api` 文档):`UpiCardFacade.queryCard`——查会员 UPI 卡信息与激活状态;传 deviceId+IP 时支持开卡(部分会员类型有地域限制)。
- **读写的表**:待补

## 关键方法 / 入口
- 待补(本窗口未单独抽取 Dubbo/RPC 方法级)。

## 测试要点 / 排障 / 常见问题
- 待补(QA 视角:怎么测、已知坑、典型故障与定位)。

## 相关流程 / 场景 / 排障(反向)
本服务涉及的流程/场景/排障(由对方 `related_services` 指向,反向汇总):
- [[flow_unionpay_card_activation]](流程:UnionPay 银联卡激活端到端流程)
- [[scn_unionpay_usage]](场景:UnionPay 三入口使用场景(Money / 付款码 / 扫商户码 + 外币))

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp153` · domain=`payment-core`。
