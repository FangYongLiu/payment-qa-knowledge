---
id: svc_cns
object_type: Service
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp289
name: cns
dev_owner: Yu.Tang,Xiaoyu.Sun
aliases: [gp289_cns]
related_services: [svc_member, svc_csimple, svc_cms]
related_tables: []
---

# cns

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp289` · domain=`payment-core`。

## 作用
（推断：客户通知 / 客户服务，调 member/csimple）  **(待核实:仅凭调用关系推断)**

## 系统中的位置
- 功能层:客服 / 内容 / 查询 / 其他 (CS / Content / Query / Misc)
- 业务域:`payment-core`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_member]] member（会员 / 账户核心） · 19562098 次 · high
- [[svc_csimple]] csimple · 613391 次 · high
- [[svc_cms]] cms（内容 / 配置管理） · 123 次 · high

## 涉及的 API / 数据库表
- **暴露 API**(Dubbo,来源 `cns-dubbo-api` 文档):**统一通知平台**——`NotificationFacade.notify`(同步发通知)、`NotificationManageFacade`(后台配置:事件路由 `saveEventConfig`/`pageEventConfig`、TodoCard `saveCardConfig`、公众号 `saveOfficialAccountNotifyConfig`、派发审计 `pageCardNotifyDispatch`)。另支持 RabbitMQ 异步入口(exchange `exchange.cns.notification`)。
- **读写的表**:通知事件/卡片/派发记录配置(具体对象待补)。

## 关键方法 / 入口
- 待补(本窗口未单独抽取 Dubbo/RPC 方法级)。

## 测试要点 / 排障 / 常见问题
- 待补(QA 视角:怎么测、已知坑、典型故障与定位)。

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp289` · domain=`payment-core`。
