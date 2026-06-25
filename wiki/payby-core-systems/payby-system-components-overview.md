---
title: PayBy系统组件架构总览
domain: payby-core-systems
kind: wiki_page
slug: payby-system-components-overview
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:01fbd2ca-cbb4-473c-b223-7a5c516a9122
tags: []
---

# PayBy系统组件架构总览

PayBy 平台的系统组件按职责划分为五个分组：Inner、App Public、Payment Public、Common、Operation Support，每个分组下包含若干微服务组件。本页仅作组件清单整理，不涉及组件之间的依赖与调用关系。

## Inner（内部服务）

面向内部使用的服务与控制台。

- `Inner Service`
- `Inner Console`

## App Public（App 公共服务）

面向 App 端的公共能力组件。

- `pcm`
- `pcs`
- `pns`

## Payment Public（支付公共服务）

支付域对外/对内开放的公共服务集合。

- `pbs`
- `css`
- `custom`
- `grc`
- `marketing`
- `nffs`

## Common（通用基础服务）

跨业务域复用的通用能力组件。

- `acs`
- `cmsii`
- `mns`
- `voucher`
- `shortlink`
- `ma`
- `kyc`
- `protocol`
- `outman`
- `supplier`
- `dpm`

## Operation Support（运营支撑）

支撑运营与基础配置的服务。

- `basis`
- `csc`
- `basis-cms`
