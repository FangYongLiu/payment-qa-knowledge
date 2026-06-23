---
title: PayBy核心系统架构总览
domain: payby-core-systems
kind: wiki_page
slug: payby-core-systems-architecture
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:6560108c-b5bd-40cc-9265-f720aa6f7119
tags: []
---

# PayBy核心系统架构总览

PayBy 核心系统采用分层架构，自上而下分为应用层、支付层、渠道层，并由业务工具与管理组件横向支撑。组件依赖方向为：应用层 → 支付层 → 渠道层。

## 分层与图例约定

- 橙色：业务组件（应用层 / 支付层 / 渠道层）
- 绿色：业务工具组件
- 蓝色：管理组件

## 应用层（Application Layer）

面向外部接入与业务入口的组件集合：

- 收单网关 `mas`
- 会员网关 `mgs`
- 企业钱包 `merchant-wallet`
- P2P交易 `p2p`
- 基金交易 `fundtrade`
- 资金托管站点 `hostweb`
- 支付工具网关 `pas`
- 文件交易 `filetrade`
- 商户配置 `acs`
- 凭证服务 `voucher`
- 商户通知 `pns`
- 收银台 `cashdesk`
- 文件网关 `filegateway`

## 支付层（Payment Layer）

承载交易撮合、账户与资金动账等核心支付能力：

- 交易服务 `trade`
- 充值服务 `deposit`
- 出款服务 `fundout`
- 支付引擎 `payment`
- 支付前置 `pfs`
- 储值 `dpm`
- 会员账户 `ma`
- 统一查询 `query`

## 渠道层（Channel Layer）

对接外部银行、备付金及验证等渠道：

- 资金渠证管理 `cmf`
- 资金渠道 `bcss`
- 银行存管 `custody`
- 银行储值 `cdpm`
- 备付金监管 `pvs`
- 外部验证渠道 `outman`
- 渠道回调网关 `fcw`

## 业务工具（Business Tools）

为核心链路提供横向支撑能力：

- 运营对账 `csa`
- 算费 `pbs`
- 消息发送 `mns`
- 运营监控 `sql-mon`

## 管理组件

图例中以蓝色标识，用于系统管理域（原文未列出具体组件清单）。

## 组件依赖关系

- 应用层依赖支付层：业务入口（如 `mas`、`mgs`、`cashdesk` 等）调用支付层的 `trade`、`deposit`、`fundout`、`payment`、`ma` 等能力。
- 支付层依赖渠道层：支付/出款/充值通过 `bcss`、`custody`、`cdpm`、`pvs`、`outman`、`fcw` 等对接外部资金与验证渠道。
- 业务工具组件横向服务于上述各层（对账、算费、消息、监控）。
