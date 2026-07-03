---
id: reference_rate_alert_feature_overview
object_type: Reference
name: Rate Alert 汇率提醒功能说明
aliases: [rate-alert-feature-overview]
domain: remittance
status: active
owner: lei.pan
reviewer: lei.pan
source_type: wiki
source_ref: wiki:7374f315-8e43-4820-84b6-2977d1fb0287
tags: [remittance, wiki-overview]
related_services: [svc_remittance]
related_tables: [tbl_remittance_t_exchange_rate_history, tbl_remittance_t_exchange_rate_record, tbl_remittance_t_rate_alert]
---


# Rate Alert 汇率提醒功能说明

Rate Alert（汇率提醒）允许用户设定目标汇率，当市场汇率达到或超过目标值时，系统主动通知用户，帮助其在理想时机完成汇款。

## 功能定义

- 用户自行设置目标汇率值。
- 当市场汇率达到或超过该目标值时，系统通过消息或推送通知方式提醒用户。

## 触发逻辑

- 由定时任务持续监控数据库中已存的汇率数据。
- 比对维度：按 **国家币种** 下各 **模式** 的 **最大汇率**。
- 当最大汇率与用户设定的目标值满足条件时，触发提醒。

## 业务价值

- 提升用户黏性。
- 帮助用户把握最佳汇率时机完成汇款。

## 功能入口

- 位置：汇款首页
- 触点：右上角 **闹铃 icon**
