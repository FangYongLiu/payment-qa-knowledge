---
title: PayBy系统组件架构图与模块分组
domain: payby-core-systems
kind: wiki_page
slug: payby-system-components-architecture
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:93d886c6-6fb5-4a83-8aba-0c094c356eab
tags: []
---

# PayBy系统组件架构图与模块分组

PayBy 系统组件按功能域划分为五个分组：Inner（内部）、App Public、Payment Public、Common、Operation Support。各分组以 UML 组件图形式呈现，仅表达模块归属，不包含组件之间的依赖连线或接口标注。

## Inner（内部组件）

面向内部使用的服务与控制台：

- Inner Service
- Inner Console

## App Public（标记 M）

- pcm
- pcs
- pns

## Payment Public

支付公共域组件：

- pbs
- css
- custom
- grc
- marketing
- nffs

## Common（公共能力）

通用基础能力组件：

- acs
- cmsii
- mns
- voucher
- shortlink
- ma
- kyc
- protocol
- outman
- dpm

## Operation Support（标记 M）

运营支撑组件：

- basis
- csc
- basis-cms

## 图示说明

- 所有组件均使用 `«component»` 构造型，统一浅青/蓝绿色样式。
- 组件之间**未绘制任何连接线、依赖关系或接口**，图示仅传达模块的分组归属。
- App Public 与 Operation Support 两个分组在原图中带有 "M" 标识。
