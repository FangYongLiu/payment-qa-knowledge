---
title: PayBy 系统组件架构图
domain: payby-core-systems
kind: wiki_page
slug: payby-system-components-architecture
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:7255e24a-242f-4cb5-a0aa-d405f511b682
tags: []
---

# PayBy 系统组件架构图

本页描述 PayBy 平台的整体组件架构,通过 UML 组件图按分包(Merchant、SDK、Static Resource、Gateway、Acquire、Personal、App Public)展示各服务的归属与依赖关系。

## 组件类型图例

架构图中的组件按颜色区分为四类:

- **Partner Service**(白色):合作伙伴/外部接入侧服务
- **Jar Component**(橙色):以 Jar 包形式提供的组件
- **Static Resource**(黄色):静态资源
- **Inner Service**(青色):内部服务

均以 `<<component>>` 构造型标识。

## 包与组件清单

### Merchant(商户接入)
Partner Service:
- Administrator
- Smart POS
- Smart Box

### SDK Platform
- app-sdk(Jar Component)
- Platform Service(Partner Service)

### Static Resource
- hive-merchant
- hive-m-topay

### Gateway(网关,Inner Service)
- pos-gateway
- xbh-gateway
- cgs
- sgs

### Acquire(收单,Inner Service)
- software-management
- device
- acquire-service
- merchant-console-frontend
- merchant

### Personal(个人侧,Inner Service)
- pcm
- socialpay
- personal
- transfer

### App Public
- pts

## 关键依赖关系

组件之间通过虚线箭头表示依赖,主要链路如下:

### 接入层 → 网关/静态资源
- Administrator → hive-merchant
- Smart POS → pos-gateway
- Smart Box → xbh-gateway
- app-sdk → cgs
- Platform Service → sgs

### 网关 → 后端服务
- pos-gateway、xbh-gateway → acquire-service,并直达 Acquire 内部组件 device、software-management
- cgs → personal、socialpay、pcm、pts
- sgs → personal、transfer

### Acquire 内部依赖
- merchant-console-frontend → hive-m-topay(静态资源)、merchant、acquire-service、device
- acquire-service → device、merchant、pcm
- software-management → device

### Personal 内部依赖
- personal → transfer
- socialpay(原文未完整列出后续依赖)

> 注:本图为整体组件视图,具体业务流程与接口细节请参见各服务的详细文档。
