---
title: 风控核身规则配置指南(Basis)
domain: risk-control
kind: wiki_page
slug: risk-control-identity-rule-config
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:942ea0be-c944-494f-a4e2-8def55b87af5
tags: []
---

# 风控核身规则配置指南(Basis)

本文介绍在 SIM 环境下，通过 Basis 系统配置风控核身规则（例如 3DS 验证）的操作步骤，以及规则生效所需的审核与缓存清理方法。

## 背景

支付业务测试中，是否触发 3DS 核身验证由风控决策。通过在 Basis 中配置 Identity Rule，可控制特定支付场景下是否出 3DS。

## 配置入口

路径：`Basis => Risk Control => Risk Event => Identity Rule Management`

## 添加核身规则

在 Identity Rule Management 页面新增规则，主要字段如下：

- **EventType**：风控事件类型，例如 `PAYMENT`
- **IdentityRule**：规则条件，例如 `payAmount>=10`
- **IdentityCheckType**：多规则条件之间的关系，例如 `&&`
- **IdentityType**：要出示的核身方式，例如 `THREEDS`
- **Priority**：优先级，值越小优先级越高

## 审核核身规则

核身规则的以下操作都需要走审核流程：

- 新增
- 生效
- 停用

## 清除 Redis 缓存使规则生效

审核通过后，需清除缓存才能使规则真正生效。

- 缓存 key：`gp079_grc-check-identity-provider`
- 提供两种清除方式（方法 1 / 方法 2），任选其一执行即可

清除后，新配置的核身规则即开始生效。
