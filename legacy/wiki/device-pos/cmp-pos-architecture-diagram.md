---
title: CMP POS产品架构图说明
domain: device-pos
kind: wiki_page
slug: cmp-pos-architecture-diagram
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:4eb7df9a-1eeb-4ff6-890d-519143ccb0e5
tags: []
---

# CMP POS产品架构图说明

本页基于 `cmp component` 架构图，描述 CMP/POS 产品从终端 App、网关、应用中台、基础设施到渠道层的组件分层与依赖关系。

## 分层总览

整体架构自上而下分为五层：

- **App 层**：商户侧终端与 POS 应用
- **网关层**：POS 流量入口
- **应用层 / 中台层**：收银、收单、交易与计费
- **基础设施**：加解密硬件
- **渠道层**：对外渠道接入与卡组织对接

## App 层

- `merchant mis`：商户 MIS 系统
- `payby pos`：POS 终端应用
- `merchant mis` 通过 **usb/bluetooth** 连接 `payby pos`

## 网关层

- `pos-gateway`：POS 网关
- `payby pos` 通过 **https(sim/wifi)** 接入 `pos-gateway`

## 应用层 / 中台层

包含组件：

- `pos-cashier`：POS 收银
- `acquire2`：收单
- `trade/pfs`：交易 / PFS
- `counter`：计费 / counter

依赖关系：

- `pos-gateway` → `pos-cashier`
- `pos-gateway` → `acquire2`
- `acquire2` → `pos-cashier`
- `pos-cashier` → `trade/pfs`
- `acquire2` → `trade/pfs`
- `trade/pfs` → `counter`

## 基础设施

- `hsm`：加解密硬件模块
- `trade/pfs` ↔ `hsm`
- `cmf` 同样接入 `hsm`

## 渠道层

包含组件：

- `cmf`：渠道前置
- `onboarding`：入网
- `qpay-ni2`：NI 渠道适配
- `ni-socket`：NI 长连接通道

依赖关系：

- `trade/pfs` → `cmf`
- `counter` → `cmf`
- `cmf` → `qpay-ni2`
- `onboarding` → `qpay-ni2`
- `qpay-ni2` → `ni`（NI 卡组织 / 渠道方）
