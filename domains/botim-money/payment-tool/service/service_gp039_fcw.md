---
id: svc_fcw
object_type: Service
domain: payment-tool
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp039
name: fcw
dev_owner: Guoyou.Ma
aliases: [gp039_fcw]
related_services: [svc_cmf, svc_remittance, svc_visii]
related_tables: []
---

# fcw

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp039` · domain=`payment-tools`。

## 作用
前置渠道网关（Front Channel Web）—— 3DS 跳转 / 渠道通知页；下游 cmf/remittance

## 系统中的位置
- 功能层:接入网关 / 前端 BFF (Gateway / Frontend)
- 业务域:`payment-tools`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_cmf]] cmf（渠道管理与资金） · 30176 次 · high
- [[svc_remittance]] remittance（跨境汇款核心） · 718 次 · high
- [[svc_visii]] visii · 118 次 · high

## 参与的业务场景(cgs 回归)
- §1. 直连支付 / 预授权 / DCC（toB，`test_direct_pay` / `test_pre_auth_capture` / `test_bpg_paypage`）
- §4. 卡渠道入金 3DS（`test_mpgs_fundIn` / `test_cko_fundIn`）

## 涉及的 API / 数据库表
- **暴露/相关 API**:待补
- **读写的表**:待补

## 关键方法 / 入口
- 待补(本窗口未单独抽取 Dubbo/RPC 方法级)。

## 测试要点 / 排障 / 常见问题
- 待补(QA 视角:怎么测、已知坑、典型故障与定位)。

## 相关流程 / 场景 / 排障(反向)
本服务涉及的流程/场景/排障(由对方 `related_services` 指向,反向汇总):
- [[auto_online_business_zand_mock_vs]](自动化:ZAND Mock VS 回调工具(Zand.java))
- [[flow_zand_fundout]](流程:ZAND渠道出款端到端流程(SP/SQ/VS))
- [[scn_online_business_zand_fundout]](场景:ZAND渠道出款测试场景(TC-001~010))
- [[ts_zand_fundout]](排障:ZAND渠道出款常见故障排查)

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp039` · domain=`payment-tools`。
