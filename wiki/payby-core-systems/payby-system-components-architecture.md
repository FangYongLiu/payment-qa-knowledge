---
title: PayBy系统组件架构图
domain: payby-core-systems
kind: wiki_page
slug: payby-system-components-architecture
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:28cb95dc-7145-4e87-98a4-e48812a0fc2b
tags: []
---

# PayBy系统组件架构图

PayBy 支付系统按业务职责划分为五个域：**交易**、**支付**、**会员账户**、**资金渠道**、**银行**，由内部应用、未改造应用与合作方应用三类组件协作完成支付链路。

## 图例（组件类型）

- **内部应用**：浅青色
- **未改造**：红色（遗留系统，待重构）
- **合作方应用**：白色

## 业务域与组件构成

### 交易（Trade）

均为内部应用：

- trade
- deposit
- fundout
- cashesk
- authpay
- query

### 支付（Payment）

均为内部应用：

- pfs-payment
- payment

### 会员账户（Member Account）

均为内部应用：

- ma
- dpm

### 资金渠道（Fund Channel）

- cmf（内部应用）
- fundchannel-mock（内部应用）
- fundchannel-xxx（内部应用）
- fcw（未改造）

### 银行（Bank）

- bank（合作方应用）

## 组件依赖关系

组件间以虚线依赖箭头连接，主要链路如下：

### 交易域内部及对支付的依赖

- trade → pfs-payment
- deposit → trade（trade 与 deposit/cashesk 之间存在反向虚线连接）
- cashesk → authpay
- cashesk → pfs-payment（反向链接）

### 支付域到下游

- pfs-payment → payment → cmf
- pfs-payment → ma
- payment → dpm
- ma → dpm

### 资金渠道到银行

- cmf → fundchannel-mock
- cmf ↔ fundchannel-xxx
- fundchannel-xxx → bank
- cmf → fcw
- fcw ↔ bank（bank 通过虚线反向连接 fcw）

## 整体调用走向

由交易域组件发起请求，经支付域（pfs-payment / payment）路由至会员账户（ma / dpm）记账与资金渠道（cmf）出款，再由 fundchannel-xxx 或遗留组件 fcw 对接合作方 bank 完成与银行的资金交互。
