---
id: svc_ppcenter
object_type: Service
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp047
name: ppcenter
dev_owner: Yadong.Lu
aliases: [gp047_ppcenter]
related_services: [svc_member, svc_acs, svc_contract]
related_tables: []
---

# ppcenter

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp047` · domain=`payment-core`。

## 作用
产品中心（商户开通产品状态 queryMerchantOpenedProductStatus，被 acquire/device/merchant-fundout 调用）

## 系统中的位置
- 功能层:营销 / 产品 / 报价 (Marketing / Product / Quote)
- 业务域:`payment-core`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_member]] member（会员 / 账户核心） · 1820 次 · high
- [[svc_acs]] acs（反欺诈 / 风控 + 渠道密钥） · 102 次 · high
- [[svc_contract]] contract · 14 次 · high

**被调用(上游)—— 这些服务调用本服务:**
device, acquireii, merchant-fundout

## 参与的业务场景(cgs 回归)
- §1. 直连支付 / 预授权 / DCC（toB，`test_direct_pay` / `test_pre_auth_capture` / `test_bpg_paypage`）

## 关键方法 / 入口
queryMerchantOpenedProductStatus

## 涉及的 API / 数据库表
- **暴露/相关 API**:待补
- **读写的表**:待补

## 测试要点 / 排障 / 常见问题

**UAT Kibana 7d 错误观测**(自动回归 + UAT 流量,app_id=`ppcenter`):
- ERROR 102 次,主要:`ConfigDefineServiceImpl`×22
- WARN 11 次(均为基础设施噪声)
- ⚠️ 频次可能含 UAT 测试数据噪声,**真坑 vs 噪声需人工确认**;高频项见域级排障对象。
- 更多 QA 校验点(怎么测 / 已知坑 / 典型故障定位)待补。
## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp047` · domain=`payment-core`。
