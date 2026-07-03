---
id: svc_authpay
object_type: Service
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp034
name: authpay
dev_owner: Guoyou.Ma
aliases: [gp034_authpay]
related_services: []
related_tables: []
related_scenarios: [scn_online_business_auto_debit]
---

# authpay

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp034` · domain=`payment-core`。

## 作用
授权支付 / 免密代扣执行（被 cashier/cashdesk/trade 调用）

## 系统中的位置
- 功能层:收单 / 收银 (Acquiring / Cashier)
- 业务域:`payment-core`

## 关联关系

**被调用(上游)—— 这些服务调用本服务:**
cashierii, cashdesk-api, tradeii

## 参与的业务场景(cgs 回归)
- §1. 直连支付 / 预授权 / DCC（toB，`test_direct_pay` / `test_pre_auth_capture` / `test_bpg_paypage`）
- §2. 收银台 / 收银（`test_bpg_paypage` 收银侧、cashier 用例）

## 涉及的 API / 数据库表
- **暴露/相关 API**:Dubbo `queryPayAuthority`(`QueryPayAuthorityRequest`)、`payAuthority`(`PayAuthorityRequest`);被 [[svc_cashierii]]/[[svc_cashdesk_api]]/[[svc_tradeii]]/[[svc_deduct]] 调。
- **读写的表**:支付鉴权 商户组/方案/策略配置(具体对象待补)。

## 关键方法 / 入口(UAT 实测)
- **支付鉴权**:`queryPayAuthority` / `payAuthority` —— 按**商户组 → 方案 → 策略**匹配,输出可用支付模式。实测:`商户组为ID [87, 2, 1]` → `匹配方案列表 [137, 15]` → `支付鉴权通过,支付模式[QPAY]`。
- 免密代扣执行:AUTODEBIT/收银免密支付前的鉴权关口。

## 测试要点 / 排障 / 常见问题(UAT 实测)
- **鉴权关口**:支付前 authpay 判定商户组/方案/策略是否允许该支付模式(QPAY 等);鉴权失败即支付被拦。`PayAuthorityRequest` 含 payMethodCode/payChannelCode/productCode/paySceneCode。
- **怎么测/定位**:不同商户组/产品/场景组合下鉴权结果与支付模式;支付失败先看 `支付鉴权成功` 是否出现 + 匹配的方案/策略 ID。
- 是收银([[svc_cashierii]]/[[svc_cashdesk_api]])、交易([[svc_tradeii]])、代扣([[svc_deduct]])共用的鉴权服务。

## 相关流程 / 场景 / 排障(反向)
本服务涉及的流程/场景/排障(由对方 `related_services` 指向,反向汇总):
- [[auto_online_business_auto_debit]](自动化:自动代扣自动化)
- [[flow_cashier_payment]](流程:收银台 / 收单卡支付端到端流程（含退款）)
- [[scn_online_business_auto_debit]](场景:自动代扣 / 签约 (Auto Debit))

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp034` · domain=`payment-core`。
