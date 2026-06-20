---
title: 风控核身规则配置指南(3DS)
domain: risk-control
kind: wiki_page
slug: risk-control-identity-rule-config
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/1057685568
tags: []
---

# 风控核身规则配置指南(3DS)

本页说明如何在 SIM 环境的 Basis 系统中，通过配置风控核身规则来控制支付场景是否触发 3DS 核身验证。

## 背景

在支付测试中，部分场景需触发 3DS 验证，部分场景无需触发；是否出 3DS 核身由风控规则决定。本指南介绍在 SIM 环境配置该规则的方法。

## 配置路径

Basis => Risk Control => Risk Event => Identity Rule Management

## 添加核身规则

在上述路径下新增规则，关键字段：

- **EvenType**：风控事件，例如 `PAYMENT`
- **IdentityRule**：规则条件，例如 `payAmount>=10`
- **IdentityCheckType**：多规则条件之间的关系，例如 `&&`
- **IdentityType**：要出示的核身方式，例如 `THREEDS`
- **Priority**：优先级，值越小优先级越高

## 审核流程

核身规则的以下操作均需审核：

- 新增
- 生效
- 停用

## 清除 Redis 缓存

规则审核通过后，需清除以下缓存才会真正生效：

- 缓存 key：`gp079_grc-check-identity-provider`

清理方式提供两种（方法 1 / 方法 2），任选其一即可使配置生效。
