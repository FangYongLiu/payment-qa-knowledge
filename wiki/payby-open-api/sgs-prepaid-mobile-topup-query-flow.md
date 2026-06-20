---
title: SGS预付费手机充值查询API调用时序
domain: payby-open-api
kind: wiki_page
slug: sgs-prepaid-mobile-topup-query-flow
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:39cd2785-6631-4df8-bea8-305fdf9c04b6
tags: []
---

# SGS预付费手机充值查询API调用时序

本页描述 partner 调用 SGS 预付费手机充值查询接口 `/lifecenter/goods/v1/query-prepaid-mobile-top-up` 的内部调用链路：sgs 将请求委派给 life-center，由其依次解析 partner、host app 并查询充值商品。

## 调用入口

- 调用方：partner
- 入口接口：`/lifecenter/goods/v1/query-prepaid-mobile-top-up`
- 接收方：`sgs`，由 `sgs` 转发至 `life-center` 处理

## life-center 内部处理顺序

life-center 接收到调用后，按以下顺序执行：

1. **query matching partner**（自调用）
   - 调用 `acs` 的 `SettingFacade#getMerchantSetting` 获取商户配置
2. **query host app**（自调用）
   - 调用 `member` 的 `IConfigFacade#getByTypeAndValue` 解析宿主应用
3. **查询手机充值商品**
   - 调用 `market-goods` 的 `GoodsFacade#queryMobileTopUp`
   - `market-goods` 进一步调用 `supplier` 的 `SupplierHandleFacade#queryChannelsByAccount` 查询供应商渠道

## 返回链路

- `life-center` → `sgs`（返回结果）
- `sgs` → `partner`（返回结果）

## 涉及服务一览

| 服务 | 作用 |
| --- | --- |
| sgs | 对外 API 入口，委派给 life-center |
| life-center | 编排：解析 partner、host app，并发起商品查询 |
| acs | 提供 `SettingFacade#getMerchantSetting`，用于匹配 partner |
| member | 提供 `IConfigFacade#getByTypeAndValue`，用于查询 host app |
| market-goods | 提供 `GoodsFacade#queryMobileTopUp`，查询手机充值商品 |
| supplier | 提供 `SupplierHandleFacade#queryChannelsByAccount`，查询渠道 |
