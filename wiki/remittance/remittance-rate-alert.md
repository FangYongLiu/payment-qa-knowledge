---
title: 汇率提醒(Rate Alert)功能说明
domain: remittance
kind: wiki_page
slug: remittance-rate-alert
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/1268547799
tags: []
---

# 汇率提醒(Rate Alert)功能说明

汇率提醒（Rate Alert）允许用户预设目标汇率，当市场汇率达到或超过该目标值时，系统主动通过消息或推送通知用户，帮助其在最佳时机完成汇款。

## 功能定义

- 用户自行设置目标汇率（target rate）。
- 当市场汇率满足目标条件时，系统通过消息或推送通知提醒用户。

## 触发逻辑

- 由定时任务（定时轮询）驱动监控。
- 监控对象：数据库中**各国家币种**下、**各模式**的**最大汇率**。
- 比对方式：将当前最大汇率与用户设定的目标值进行比对。
- 触发条件：当前汇率达到或超过用户目标值时，触发提醒。

## 业务价值

- 提升用户黏性。
- 引导用户在最佳汇率时机完成汇款。

## 功能入口

- 位置：**汇款首页**右上角的**闹铃 icon**。
