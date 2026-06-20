---
title: 系统组件架构与依赖关系
domain: payby-core-systems
kind: wiki_page
slug: system-components-architecture
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:e7a58d61-3be2-4919-9611-113cb875997c
tags: []
---

# 系统组件架构与依赖关系

本页描述 merchant-portal 业务域所依赖的系统组件分类（内部服务、内部控台、Jar 组件、第三方服务、第三方控台）及其相互依赖关系，并给出业务调用链的分层视图。

## 组件分类图例

组件按用途分为五类，在架构图中以颜色区分：

- **Inner Service**（内部服务）
- **Inner Console**（内部控台）
- **Jar Component**（Jar 组件）
- **3rdParty Service**（第三方服务）
- **3rdParty Console**（第三方控台）

## 业务分层架构

从外部调用方到中台的整体请求路径，按层划分如下：

### 外部调用方

- **merchant_system**：外部商户系统，作为调用入口。

### 网关层（Gateway Layer）

- **sgs**
- **merchant-frontend**

### 业务层（Business Layer）

- **acquireii**

### 中台（Middle Platform）

- **tradeii**：交易中台，处于中台核心位置
- **grc**：风控相关组件
- **pfs**：支付/资金相关组件

### 调用链关系

请求自上而下流转（箭头方向表示「依赖/调用」）：

- merchant_system → sgs
- sgs → merchant-frontend
- merchant-frontend → acquireii
- acquireii → tradeii
- tradeii → grc
- tradeii → pfs

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
