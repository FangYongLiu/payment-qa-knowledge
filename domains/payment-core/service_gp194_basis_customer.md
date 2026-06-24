---
id: svc_basis_customer
object_type: Service
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp194
name: basis-customer
dev_owner: Yibing.Xia
aliases: [gp194_basis-customer]
related_services: [svc_ufs2, svc_member]
related_tables: []
---

# basis-customer

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp194` · domain=`payment-core`。

## 作用
基础数据(Basis)（customer）  **(据名推断 · 待核实:无作用文字证据,但下方有观测到的调用关系)**

## 系统中的位置
- 业务域:`payment-core`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_ufs2]] ufs2（用户文件 / 数据服务） · 273 次 · med·待核实
- [[svc_member]] member（会员 / 账户核心） · 70 次 · high

## 涉及的 API / 数据库表
- **暴露/相关 API**:待补
- **读写的表**:待补

## 关键方法 / 入口
**UAT Kibana 7d INFO 观测的主要业务类**(app_id=`basis-customer`,=实际在跑的业务操作 / 入口):
- `RemittanceTransactionsService`×3,279 — 汇款交易(客户侧)
- (类名为 Dubbo/RPC 处理器/门面;次数为 7d 调用量级,反映主链路。)
## 测试要点 / 排障 / 常见问题

**UAT Kibana 7d 错误观测**(自动回归 + UAT 流量,app_id=`basis-customer`):
- ERROR 25 次,主要:`ServiceCaller`×9
- WARN 228 次(均为基础设施噪声)
- ⚠️ 频次可能含 UAT 测试数据噪声,**真坑 vs 噪声需人工确认**;高频项见域级排障对象。
- 更多 QA 校验点(怎么测 / 已知坑 / 典型故障定位)待补。
## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp194` · domain=`payment-core`。
