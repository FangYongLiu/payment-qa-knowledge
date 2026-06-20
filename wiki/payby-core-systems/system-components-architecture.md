---
title: 系统组件架构与依赖关系
domain: payby-core-systems
kind: wiki_page
slug: system-components-architecture
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:17d972e2-7c6e-42b7-b580-5d9db8f46dcd
tags: []
---

# 系统组件架构与依赖关系

本页描述 merchant-portal 业务域所依赖的系统组件分类（内部服务、内部控台、Jar 组件、第三方服务、第三方控台）及其相互依赖关系，并补充支付核心系统的整体分层架构（网关层、业务层、中台层、渠道层、业务工具层）。

## 组件分类图例

组件按用途分为五类，在架构图中以颜色区分：

- **Inner Service**（内部服务）
- **Inner Console**（内部控台）
- **Jar Component**（Jar 组件）
- **3rdParty Service**（第三方服务）
- **3rdParty Console**（第三方控台）

## 整体分层架构

支付核心系统按调用链路分为以下层次，整体读取方向为：**外部客户端 → 网关层 → 业务层 → 中台层 → 渠道层 → 银行**，业务工具层作为共享支撑层贯穿底部。

### 外部接入方

- Partner Server（合作方服务器）
- 42Pay APP
- MPOS
- bank（银行，位于渠道层之外）

### Gateway（网关层）

- sgs
- cgs
- posp
- pns

接入关系：

- Partner Server → sgs
- 42Pay APP → cgs
- MPOS → posp

### Biz Service（业务层）

- Acquire Service
- Personal Service
- AuthPay

接入关系：

- sgs → Acquire Service
- cgs → Personal Service
- posp → AuthPay
- Acquire Service、Personal Service 通过虚线依赖连接到 AuthPay 所在区域

### Middle Platform（中台层）

左列：trade、fundout、deposit、ma-web
右列：pfs-payment、payment、dpm

依赖关系：

- trade、fundout、deposit → pfs-payment
- pfs-payment → payment
- payment → dpm
- 业务层组件（虚线）依赖 pfs-payment

### Channel（渠道层）

- cmf
- channel

依赖关系：

- cmf → channel
- payment → channel
- channel → bank（外部）

### Biz Tool（业务工具层，底部共享支撑）

- voucher
- Qr Code Service
- pbs
- acs
- nffs

依赖关系：

- pns（网关层）→ voucher
- AuthPay → Qr Code Service
- channel → nffs（虚线）
- voucher 内部存在反向回连

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
