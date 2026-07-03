---
id: svc_acquire2_query
object_type: Service
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp275
name: acquire2-query
subdomain: acquiring
dev_owner: Sijia.Zhang
aliases: [gp275_acquire2-query]
related_services: []
related_tables: []
---

# acquire2-query

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp275` · domain=`online-business`。

## 作用
**收单查询(读侧)**服务(gp275):承接 acquire2 的**查询类**请求(订单/退款查询),与写侧 [[svc_acquireii]] 读写分离。对应 `/sgs/api/acquire2/getOrder`、`/refund/getOrder` 等查单接口后端。

## 系统中的位置
- 功能层:收单业务线(查询读侧)
- 业务域:`online-business`

## 关联关系
读侧查询,与写侧 [[svc_acquireii]] 共库/读写分离;查单入口经 [[svc_sgs]] 网关。相关 API:[[api_sgs_acquire_get_order]] / [[api_sgs_acquire_refund_get_order]]。

## 关键方法 / 入口(UAT 实测)
- 近7d ~6.6k docs;`ExceptionInterceptor`(统一异常)+ Zookeeper/Dubbo(`ClientCnxn`)注册。方法级(具体 query facade)**待补**(本窗口未抽到)。

## 测试要点 / 排障 / 常见问题
- 查单一致性:getOrder / refund/getOrder 返回与写侧订单状态一致;merchantOrderNo / orderNo 二选一。
- 读写分离下的**查询延迟**边界(刚下单立即查)。

## 相关流程 / 场景 / 排障(反向)
本服务涉及的流程/场景/排障(由对方 `related_services` 指向,反向汇总):
- [[ts_acquire_order_slow_sql]](排障:收单订单查询慢SQL(t_acquire_order 大商户时间范围查询))

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp275` · domain=`online-business`。

## 涉及的表(DB)
本服务为收单查询,读 `acquireii` 库(不拥有),主要查 [[tbl_acquireii_t_acquire_order]] · [[tbl_acquireii_t_payment_info]] · [[tbl_acquireii_t_refund_order]]。
