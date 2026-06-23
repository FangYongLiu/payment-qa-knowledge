---
title: 系统组件架构与依赖关系
domain: manual-fund-settlement
kind: wiki_page
slug: system-components-architecture
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:e331346b-3889-40cb-b35b-0045683126a5
tags: []
---

# 系统组件架构与依赖关系

本页描述系统所依赖的组件分类（内部服务、内部控台、Jar 组件、第三方服务、第三方控台）及其相互依赖关系，并涵盖 settlement 产品在 cmp webservice 模块下的服务依赖结构。

## 组件分类图例

组件按用途分为五类，在架构图中以颜色区分：

- **Inner Service**（内部服务）
- **Inner Console**（内部控台）
- **Jar Component**（Jar 组件）
- **3rdParty Service**（第三方服务）
- **3rdParty Console**（第三方控台）

## Jar 组件（Jar Component）

提供基础能力与中间件接入的 Jar 包：

- beacon
- basic-lang
- basic-util(dep)
- pmock
- ues-client
- sequence-util
- monitor-starter
- mq-stater
- dubbo-starter
- job-starter
- redis-starter
- mysql-starter
- cobarclient

## 内部服务与控台

- **Inner Service**：ues、ufs

## 第三方服务（3rdParty Service）

- spring-cloud-config
- nacos
- rabbit-mq
- zookeeper
- redis
- mysql
- Alibaba Cloud

## 第三方控台（3rdParty Console）

- gitlab
- spring-boot-admin
- dubbo-admin
- elasticjob-console

## 组件依赖关系

各组件之间的依赖（箭头方向表示「依赖于」）：

- beacon → basic-lang
- monitor-starter → spring-cloud-config
- monitor-starter → nacos
- spring-cloud-config → gitlab
- spring-boot-admin → nacos
- mq-stater → rabbit-mq
- dubbo-starter → zookeeper
- job-starter → zookeeper
- dubbo-admin → zookeeper
- elasticjob-console → zookeeper
- redis-starter → redis
- ues-client → ues
- ues → redis
- ues → mysql
- mysql-starter → mysql

## settlement 产品架构（cmp webservice）

在 cmp webservice 模块下，`settlement` 作为顶层 Web 服务，依赖（«use» / dependency）六个下游服务组件。六个下游组件之间互不连接，均为 settlement 的同级被依赖方。

依赖关系（settlement → 下游）：

- settlement → merchant
- settlement → ufs
- settlement → counter
- settlement → pbs
- settlement → statement
- settlement → ma

> 注：此处的 `ufs` 与本页"内部服务与控台"小节中列出的 Inner Service `ufs` 为同一组件。
