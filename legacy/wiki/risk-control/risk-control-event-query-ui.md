---
title: 风控风险事件查询界面说明
domain: risk-control
kind: wiki_page
slug: risk-control-event-query-ui
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:1cf37880-ad93-4137-8bce-fefeb74766ba
tags: []
---

# 风控风险事件查询界面说明

本页介绍风控后台「风险事件查询」页面的筛选条件、结果字段与可执行操作，便于在风险事件排查时快速定位目标事件。

## 页面定位

- 页面标题：风险事件查询
- 用途：按接入点、时间、业务字段等条件检索风险事件，并支持后续处置动作

## 顶部主筛选条件

支持以下条件组合：

- 接入点：下拉选择，例如 `CP-GR-000002 :支付事件反欺诈`
- 事件ID
- 分值>=
- 分值<
- 规则编号
- 请求时间：时间区间选择

注意：**关联查询条件之间是 AND 的关系**。

## 业务字段筛选

下方筛选区提供按业务字段精确查询的输入框，每个字段下方带有勾选框（用于结果列展示或匹配控制）。字段包括：

- bindCardDays
- greenPointUsed
- tid
- payAmount
- payerMemberId
- payeeMemberId
- customerEventType
- eventType
- bizProductCode
- transactionId
- payChannel
- paymentOrderNo

## 操作按钮

- 搜索：按当前筛选条件查询事件
- 添加名单库：将选中事件加入名单库
- 人工审核：对选中事件发起人工审核流程

## 结果列表字段

结果表格包含以下列：

- 选中全部（多选框）
- 事件ID
- 接入点
- 业务字段列：bindCardDays、greenPointUsed、tid、payAmount、payerMemberId、payeeMemberId、customerEventType、eventType、bizProductCode、transactionId、payChannel、paymentOrderNo
- 分值
- 规则
- 请求时间
- 耗时(ms)
- 标签
- 事件日志
- 操作
