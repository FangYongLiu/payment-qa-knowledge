---
title: PayBy系统组件依赖总览
domain: payby-core-systems
kind: wiki_page
slug: payby-system-components-overview
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:c0b3e3aa-efc5-446f-b098-a958b9fbe964
tags: []
---

# PayBy系统组件依赖总览

本页梳理 PayBy 体系内的组件分类（内部服务、内部控台、Jar 组件、第三方服务、第三方控台）及其依赖关系，来源为 System Components 组件图。

## 图例与分类

组件按颜色编码区分为五类：

- **Inner Service**（内部服务）
- **Inner Console**（内部控台）
- **Jar Component**（Jar 组件）
- **3rdParty Service**（第三方服务）
- **3rdParty Console**（第三方控台）

## Jar 组件清单

PayBy 内部封装的可复用 Jar 组件：

- beacon
- basic-lang
- basic-util
- monitor-starter
- mq-stater
- dubbo-starter
- job-starter
- redis-starter
- mysql-starter
- ues-client
- sequence-util
- cobarclient

> 注：消息组件原图标识为 `mq-stater`（非 starter）。

## 内部服务

- ues
- ufs

## 第三方服务

- gitlab
- nacos
- rabbit-mq
- zookeeper
- redis
- mysql
- Alibaba Cloud
- spring-cloud-config

## 第三方控台

- spring-boot-admin
- dubbo-admin
- elasticjob-console

## 关键依赖关系

组件图中以虚线箭头标注的依赖：

- `beacon` → `basic-lang`
- `monitor-starter` → `spring-cloud-config` → `gitlab`
- `monitor-starter` → `nacos`
- `mq-stater` → `nacos`
- `mq-stater` → `rabbit-mq`
- `dubbo-starter` → `zookeeper`
- `job-starter` → `zookeeper`

## 说明

- Jar 组件普遍依赖对应的第三方基础设施（如 mq → rabbit-mq、dubbo → zookeeper、job → zookeeper）。
- 配置类依赖通过 `spring-cloud-config` 接入 `gitlab`。
- 服务注册与配置中心统一接入 `nacos`。
