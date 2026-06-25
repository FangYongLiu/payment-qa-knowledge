---
id: flow_remittance_life_center_sgs_query
object_type: Flow
name: Life-Center SGS 预付国际商品 / 后付费账单查询调用链
aliases: [life-center SGS API 处理流程, query-prepaid-international, query-postpaid-mobile-bill]
domain: remittance
status: active
owner: lei.pan
reviewer: lei.pan
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: wiki_image:8267b295-ac07-4d39-a0c6-4c8eecf43392; wiki_image:b2aa19f2-2969-4c79-adcd-9cc4deb6e51e
tags: [life-center, sgs, query, prepaid, postpaid, bill]
related_services: [svc_sgs, svc_life_center, svc_cmsii, svc_supplier, svc_market_order, svc_channel_paykii]
related_tables: []
related_scenarios: []
---

# Life-Center SGS 预付国际商品 / 后付费账单查询调用链

## 概述
partner(外部调用方)通过 [[svc_sgs]] 网关查询 Life-Center 商品的两条分层同步调用链:
① 查询预付国际商品(query-prepaid-international);② 查询后付费手机账单(query-postpaid-mobile-bill)。
[[svc_sgs]] 仅作入口转发,核心逻辑由 [[svc_life_center]] 编排,逐层委派至配置 / 订单 / 供应商 / 渠道服务,最终(后付场景)落到外部 paykii。起点 = partner 经 SGS 发起查询;终点 = 结果沿原路同步返回。

## 步骤(跨系统)

### 链路 A:预付国际商品查询
1. partner → [[svc_sgs]]:`/lifecenter/goods/v1/query-prepaid-international`
2. [[svc_sgs]] → [[svc_life_center]]:转发请求
3. [[svc_life_center]] → [[svc_cmsii]]:`ConfigurationItemFacade#match`,解析配置匹配
4. [[svc_life_center]] → [[svc_supplier]](loop:iterate all countries):`FundPreQueryFacade#providerAccountQuery`,按国家循环查询供应商账户
5. [[svc_life_center]] → [[svc_sgs]] → partner:结果同步返回

### 链路 B:后付费手机账单查询
1. partner → [[svc_sgs]]:`/lifecenter/goods/v1/query-postpaid-mobile-bill`
2. [[svc_sgs]] → [[svc_life_center]]:(无方法标签)
3. [[svc_life_center]] → [[svc_market_order]]:`LifeBillFacade#queryLifeBill`
4. [[svc_market_order]] → [[svc_supplier]]:`FundPreQueryFacade#customerOwedBillQuery`
5. [[svc_supplier]] → [[svc_channel_paykii]]:`PaykiiQueryFacade#queryAmountDue`
6. [[svc_channel_paykii]] → paykii(外部系统,终点):(无方法标签)

## 关联关系
- **经过的服务(有序)**:[[svc_sgs]] → [[svc_life_center]] →(A)[[svc_cmsii]] / [[svc_supplier]];(B)[[svc_market_order]] → [[svc_supplier]] → [[svc_channel_paykii]] → paykii(外部,待补)(= `related_services`)
- **关键表**:待补
- **关键场景**:待补

## 校验点
- 两条链路均为分层同步嵌套调用(UML activation bar);图中仅画请求方向,无 return arrow。
- 链路 A:配置匹配(cmsii `ConfigurationItemFacade#match`)先于供应商账户查询;供应商查询对所有国家循环(loop fragment)。
- 链路 B:Facade 委派层次 `LifeBillFacade`(life-center)→ `FundPreQueryFacade#customerOwedBillQuery`(market-order 调 supplier)→ `PaykiiQueryFacade#queryAmountDue`(supplier 调 channel-paykii)→ 外部 paykii。
- 入口接口均经 SGS 暴露;内部领域服务以 Facade 形式暴露。
- 业务域归属:原 wiki 标 remittance(实际跨 life-center / payment-tools,待核实归属)。
