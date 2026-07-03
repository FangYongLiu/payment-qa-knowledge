---
id: reference_payby_system_components_overview
object_type: Reference
name: PayBy系统组件架构总览
aliases: [payby-system-components-overview]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
source_type: wiki
source_ref: wiki_image:01fbd2ca-cbb4-473c-b223-7a5c516a9122
tags: [payment-core, wiki-overview]
related_services: [svc_acs, svc_basis, svc_basis_cms, svc_cmsii, svc_csc, svc_css, svc_custom, svc_kyc, svc_marketing, svc_outman, svc_pbs, svc_pcm, svc_pcs, svc_pns, svc_protocol, svc_shortlink]
related_tables: []
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
