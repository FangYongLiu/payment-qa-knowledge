---
title: Life-Center SGS 后付费账单查询API调用链
domain: remittance
kind: wiki_page
slug: life-center-sgs-query-postpaid-bill-flow
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:b2aa19f2-2969-4c79-adcd-9cc4deb6e51e
tags: []
---

# Life-Center SGS 后付费账单查询API调用链

本页描述 partner 通过 SGS 查询后付费手机账单时，跨 life-center、market-order、supplier、channel-paykii 直至外部 paykii 系统的同步分层调用时序（业务域 domain=remittance）。

## 参与方

调用链涉及以下 7 个参与者（从外到内）：

- **partner**：发起方（actor）
- **sgs**：对外 API 网关
- **life-center**
- **market-order**
- **supplier**
- **channel-paykii**
- **paykii**：外部系统终点

## 调用时序

按层级顺序的同步调用：

1. `partner → sgs`：`/lifecenter/goods/v1/query-postpaid-mobile-bill`
2. `sgs → life-center`：（无方法标签）
3. `life-center → market-order`：`LifeBillFacade#queryLifeBill`
4. `market-order → supplier`：`FundPreQueryFacade#customerOwedBillQuery`
5. `supplier → channel-paykii`：`PaykiiQueryFacade#queryAmountDue`
6. `channel-paykii → paykii`：（无方法标签，外部终端调用）

## 调用特征

- **同步调用**：每一层在 UML 序列图中显示嵌套的 activation bar，表明为同步嵌套调用。
- **分层委派**：partner 发起的 REST 请求经 SGS 网关，逐层委派至 life-center → market-order → supplier → channel-paykii，最终落到外部 paykii。
- **未绘制返回箭头**：图中仅展示请求方向，无 return arrow。

## 业务语义

- 入口接口为 SGS 暴露的后付费手机账单查询 API：`/lifecenter/goods/v1/query-postpaid-mobile-bill`。
- 内部领域服务以 Facade 形式暴露：`LifeBillFacade`（life-center）、`FundPreQueryFacade`（market-order 调 supplier）、`PaykiiQueryFacade`（supplier 调 channel-paykii）。
- 业务域归属：remittance。
