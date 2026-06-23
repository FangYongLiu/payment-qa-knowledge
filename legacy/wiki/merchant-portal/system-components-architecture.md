---
title: 系统组件架构与依赖关系
domain: merchant-portal
kind: wiki_page
slug: system-components-architecture
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:5ea6b3c2-dcd4-4c82-a7c0-e50d82d0da90
tags: []
---

# 系统组件架构与依赖关系

本页描述 merchant-portal 业务域所依赖的系统组件分类（内部服务、内部控台、Jar 组件、第三方服务、第三方控台）及其相互依赖关系。

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
