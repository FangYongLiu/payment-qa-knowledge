---
id: svc_query
object_type: Service
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp030
name: query
dev_owner: Yongxing.Cao
aliases: [gp030_query]
related_services: []
related_tables: []
---

# query

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp030` · domain=`payment-core`。

## 作用
查询 / 报表服务（被 rdgs 调用）

## 系统中的位置
- 功能层:客服 / 内容 / 查询 / 其他 (CS / Content / Query / Misc)
- 业务域:`payment-core`

## 关联关系

**被调用(上游)—— 这些服务调用本服务:**
rdgs

## 涉及的 API / 数据库表
**暴露 / 相关 API:** [[api_sgs_query_prepaid_mobile_topup]] 查询本地预付话费充值接口、[[api_pix_mpc_query_trade]] MPC查询交易接口 (/pix/mpc/v1/query-trade)、[[api_sgs_query_prepaid_international]] 查询国际预付话费接口、[[api_sgs_query_postpaid_mobile_bill]] 查询后付费话费账单接口

## 关键方法 / 入口
- 待补(本窗口未单独抽取 Dubbo/RPC 方法级)。

## 测试要点 / 排障 / 常见问题
- 待补(QA 视角:怎么测、已知坑、典型故障与定位)。

## 相关流程 / 场景 / 排障(反向)
本服务涉及的流程/场景/排障(由对方 `related_services` 指向,反向汇总):
- [[flow_life_center_mobile_topup]](流程:Life Center 话费充值端到端流程(SGS))
- [[scn_life_center_mobile_topup]](场景:Mobile Top-up 话费充值(SGS))

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp030` · domain=`payment-core`。
