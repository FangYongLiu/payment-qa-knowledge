---
title: life-center SGS API 处理流程
domain: remittance
kind: wiki_page
slug: life-center-sgs-api-process
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:8267b295-ac07-4d39-a0c6-4c8eecf43392
tags: []
---

# life-center SGS API 处理流程

本页描述查询预付国际商品场景下，partner、sgs、life-center、cmsii、supplier 之间的 API 调用时序。

## 参与方

- **partner**：调用方（外部）
- **sgs**：API 网关层
- **life-center**：业务处理中心
- **cmsii**：配置项服务
- **supplier**：供应商账户查询服务

## 调用时序

1. `partner → sgs`：`/lifecenter/goods/v1/query-prepaid-international`
2. `sgs → life-center`：转发请求
3. `life-center → cmsii`：`ConfigurationItemFacade#match`，解析配置
4. `life-center → supplier`（loop：iterate all countries）：`FundPreQueryFacade#providerAccountQuery`，按国家循环查询供应商账户
5. `life-center → sgs`：返回结果
6. `sgs → partner`：返回结果

## 关键说明

- partner 通过 SGS 暴露的接口入口发起同步请求。
- SGS 仅作为入口转发，由 life-center 编排核心逻辑。
- life-center 先调用 cmsii 的 `ConfigurationItemFacade#match` 完成配置匹配。
- 随后对所有国家进行循环（loop fragment），逐个调用 supplier 的 `FundPreQueryFacade#providerAccountQuery`。
- 结果沿 life-center → sgs → partner 路径同步返回。
