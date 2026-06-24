---
id: svc_sgs
object_type: Service
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp028
name: sgs
dev_owner: Yongxing.Cao
aliases: [gp028_sgs]
related_services: []
related_tables: []
related_scenarios: [scn_online_business_direct_pay]
---

# sgs

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp028` · domain=`payment-core`。

## 作用
(本窗口未观测到该服务的运行时活动,作用待业务补充。)

## 系统中的位置
- 业务域:`payment-core`

## 关联关系
(本窗口未观测到与其它服务的调用关系)

## 涉及的 API / 数据库表
**暴露 / 相关 API:** [[api_sgs_place_mobile_order_prepaid]] 预付话费下单接口

## 关键方法 / 入口
**UAT Kibana 7d INFO 观测的主要业务类**(app_id=`sgs`,=实际在跑的业务操作 / 入口):
- `ReceiveOrderServiceImpl`×178,517 — 收单下单受理
- `SignServiceImpl`×178,518 — 网关签名验签
- `ServerResponseUtil`×178,545 — 网关响应
- `AcsGatewayApiServiceImpl`×32,561 — ACS 风控网关
- (类名为 Dubbo/RPC 处理器/门面;次数为 7d 调用量级,反映主链路。)
## 测试要点 / 排障 / 常见问题

**UAT Kibana 7d 错误观测**(自动回归 + UAT 流量,app_id=`sgs`):
- ERROR 277 次,主要:`HandleExceptionAssist`×188
- WARN 91 次(均为基础设施噪声)
- ⚠️ 频次可能含 UAT 测试数据噪声,**真坑 vs 噪声需人工确认**;高频项见域级排障对象。
- 更多 QA 校验点(怎么测 / 已知坑 / 典型故障定位)待补。
## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp028` · domain=`payment-core`。
