---
id: svc_query
object_type: Service
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp030
name: query
dev_owner: 曹永兴
aliases: [gp030_query]
related_services: []
related_tables: []
---

# query

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp030` · domain=`service-catalog`。

## 作用
查询 / 报表服务（被 rdgs 调用）

## 系统中的位置
- 功能层:客服 / 内容 / 查询 / 其他 (CS / Content / Query / Misc)
- 业务域:`service-catalog`

## 关联关系

**被调用(上游)—— 这些服务调用本服务:**
rdgs

## 涉及的 API / 数据库表
**暴露 / 相关 API:** [[api_sgs_query_prepaid_mobile_topup]] 查询本地预付话费充值接口、[[api_pix_mpc_query_trade]] MPC查询交易接口 (/pix/mpc/v1/query-trade)、[[api_sgs_query_prepaid_international]] 查询国际预付话费接口、[[api_sgs_query_postpaid_mobile_bill]] 查询后付费话费账单接口
