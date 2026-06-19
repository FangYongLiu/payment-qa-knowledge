---
title: PayBy系统组件架构分层
domain: payby-core-systems
kind: wiki_page
slug: payby-system-components-architecture
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:d64ece4c-bc0a-4306-83d8-130d7ccc8318
tags: []
---

# PayBy系统组件架构分层

PayBy系统组件按职责划分为四个分层包：应用公共、中台公共、通用、运营管理，另有内部应用与内部管理两个顶层组件。各层之间通过依赖关系组织，上层消费下层服务。

## 顶层组件

独立于分层包之外的两个组件：

- 内部应用 (Internal Application)
- 内部管理 (Internal Management)

## 应用公共 (Application Common)

面向应用层的公共组件：

- pcs
- pns

## 中台公共 (Middle Platform Common)

中台层公共能力组件：

- pbs
- limit

## 通用 (General)

被上层依赖的通用基础组件：

- acs
- mns
- voucher
- nffs
- ma
- outman
- dpm

## 运营管理 (Operations Management)

独立的运营管理类组件：

- counter
- basis
- csc
- sqlmonitor

## 组件依赖关系

可见的依赖（虚线箭头）反映了层间消费关系：

- pns → acs（应用公共依赖通用）
- pcs → ma（应用公共依赖通用）
- limit → ma（中台公共依赖通用）
- pbs → nffs（中台公共依赖通用，另含 nffs/ma 区域的额外虚线依赖）
- ma → outman（通用层内部依赖）
- ma → dpm（通用层内部依赖）

## 分层语义

- 应用公共 与 中台公共 层均消费 通用 层提供的服务
- 运营管理 作为独立的运营层，与业务分层并列
- 内部应用 / 内部管理 在架构顶部独立分组
