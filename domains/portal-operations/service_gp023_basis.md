---
id: svc_basis
object_type: Service
domain: portal-operations
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp023
name: basis
dev_owner: Chahid
aliases: [gp023_basis]
related_services: [svc_kyc_service, svc_ufs2, svc_member, svc_merchant, svc_tradeii]
related_tables: []
---

# basis

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp023` · domain=`portal-operations`。

## 作用
基础数据(Basis)  **(据名推断 · 待核实:无作用文字证据,但下方有观测到的调用关系)**

## 系统中的位置
- 业务域:`portal-operations`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_kyc_service]] kyc-service（实名认证服务） · 17250 次 · high
- [[svc_ufs2]] ufs2（用户文件 / 数据服务） · 14895 次 · med·待核实
- [[svc_member]] member（会员 / 账户核心） · 13779 次 · high
- [[svc_merchant]] merchant（商户主数据 / 商户管理） · 232 次 · high
- [[svc_tradeii]] tradeii（交易订单引擎） · 6 次 · high

## 涉及的 API / 数据库表
- **暴露/相关 API**:待补
- **读写的表**:待补

## 关键方法 / 入口
- 待补(本窗口未单独抽取 Dubbo/RPC 方法级)。

## 测试要点 / 排障 / 常见问题
- 待补(QA 视角:怎么测、已知坑、典型故障与定位)。

## 相关流程 / 场景 / 排障(反向)
本服务涉及的流程/场景/排障(由对方 `related_services` 指向,反向汇总):
- [[flow_mpgs_manual_onboarding]](流程:MPGS 手动报备(人工录入)入驻流程)
- [[scn_merchant_fee_bearer_separation]](场景:收支分离商户配置(独立 MID 扣手续费))
- [[scn_onboarding_manual_register]](场景:MPGS 供应商人工录入报备)

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp023` · domain=`portal-operations`。
