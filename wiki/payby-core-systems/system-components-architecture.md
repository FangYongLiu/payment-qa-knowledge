---
title: 系统组件架构与依赖关系
domain: payby-core-systems
kind: wiki_page
slug: system-components-architecture
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:5750b3d7-e8e7-47c5-8d8c-d7cd82286322
tags: []
---

# 系统组件架构与依赖关系

本页描述 merchant-portal 业务域所依赖的系统组件分类（内部服务、内部控台、Jar 组件、第三方服务、第三方控台）及其相互依赖关系，并补充 cmp webservice 的分层架构视图（外部客户端 / 网关层 / 应用层）。

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

## cmp webservice 分层架构

cmp webservice 采用三层结构：**外部客户端 → 网关层（gateway layer）→ 应用层（application layer）**。

### 外部客户端（External Clients）

- merchant-console-website
- pos_device
- merchant_system
- cashier-website（依赖 merchant_system，虚线依赖）
- customer-app
- customer-website

### 网关层（Gateway Layer）

上排（服务端网关）：
- server-gateway-service
- client-gateway-service

下排（前端网关）：
- merchant-console-frontend
- pos-gateway
- iso8583-gateway
- merchant-frontend
- customer-frontend

外部客户端到网关层的依赖：
- merchant-console-website → merchant-console-frontend
- pos_device → pos-gateway（协议：https/rpc）
- merchant_system → server-gateway-service → merchant-frontend
- merchant_system → iso8583-gateway
- cashier-website → client-gateway-service
- customer-app → client-gateway-service
- customer-website → client-gateway-service → customer-frontend

### 应用层（Application Layer）

应用层组件：

- commission
- merchant-mgmt
- acquire-service 2.0
- acquire-query-service
- cash-eatm
- pns

网关层到应用层的调用：
- merchant-console-frontend → commission、merchant-mgmt、acquire-service 2.0
- pos-gateway → acquire-service 2.0
- merchant-frontend → merchant-mgmt、acquire-query-service
- customer-frontend → cash-eatm
- iso8583-gateway → ac（来源截断）

> 注：iso8583-gateway 的下游目标在原图描述中被截断，此处仅保留可确认信息。
