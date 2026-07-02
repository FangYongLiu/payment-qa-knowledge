---
id: scn_remittance_rate_alert
object_type: Scenario
name: 汇率提醒(Rate Alert)
aliases: [Rate Alert, 汇率提醒]
domain: remittance
status: active
owner: lei.pan
reviewer: lei.pan
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:AQ/1268547799
tags: [rate-alert, 汇率提醒, remittance]
related_services: [svc_remittance]
related_tables: []
related_logs: []
---

# 汇率提醒(Rate Alert)

## 触发 / 入口
- 功能入口:汇款首页右上角的闹铃 icon。
- 用户自行设置目标汇率(target rate);由定时任务(定时轮询)驱动监控,当市场汇率满足目标条件时主动通过消息或推送通知用户。

## 关联关系
- **涉及服务**:[[svc_remittance]](= `related_services`;具体承载汇率监控 / 通知的服务待补)
- **校验的表**:待补(存储各国家币种、各模式最大汇率的表)
- **相关日志**:待补

## 前置条件
- 用户处于汇款域,可设置目标汇率。
- 数据库中维护各国家币种、各模式下的最大汇率。

## 操作步骤
1. 用户在汇款首页右上角闹铃 icon 进入,设置目标汇率(target rate)。
2. 定时任务轮询监控:取数据库中各国家币种、各模式下的最大汇率。
3. 将当前最大汇率与用户设定目标值比对。
4. 当前汇率达到或超过用户目标值 → 触发提醒。
5. 系统通过消息或推送通知用户。

## DB 校验点
- 待补:各国家币种 / 各模式最大汇率的存储与更新;用户目标汇率设置记录。

## 预期结果
- 市场汇率达到或超过目标值时,用户及时收到消息 / 推送提醒,以便在最佳时机完成汇款。

## 业务价值
- 提升用户黏性;引导用户在最佳汇率时机完成汇款。

> 不确定 / 缺失的点已标「待补」。
