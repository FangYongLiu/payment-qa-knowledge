---
title: 风控事件规则配置说明
domain: risk-control
kind: wiki_page
slug: risk-control-event-rules-config
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:3a2930d0-08c7-40eb-a2da-7c86541fc95b
tags: []
---

# 风控事件规则配置说明

本页说明风控管理后台中已配置的事件规则列表，涵盖反洗钱、反欺诈、数据埋点三类业务标签，以及每条规则的传输方式与同步模式等基础属性。

## 事件规则列表

当前共配置 5 条规则，均采用接口传输（`SEND_BY_INTERFACE`）与不同步（`NO_SYNC`）模式，三项布尔开关均为 `false`。

| 编号 | 名称 | 传输方式 | 同步模式 | 备注 | 标签 |
|---|---|---|---|---|---|
| CP-GR-000001 | 反洗钱 | SEND_BY_INTERFACE | NO_SYNC | 反洗钱风险控制 | 反洗钱 |
| CP-GR-000002 | 支付事件反欺诈 | SEND_BY_INTERFACE | NO_SYNC | — | 反欺诈 |
| CP-GR-000003 | 非支付事件反欺诈 | SEND_BY_INTERFACE | NO_SYNC | — | 反欺诈 |
| CP-GR-000004 | 支付事件结果通知 | SEND_BY_INTERFACE | NO_SYNC | — | 数据埋点 |
| CP-GR-000005 | 非支付事件结果通知 | SEND_BY_INTERFACE | NO_SYNC | — | 数据埋点 |

## 字段说明

- **编号**：规则唯一标识，格式 `CP-GR-XXXXXX`。
- **传输方式**：当前所有规则均为 `SEND_BY_INTERFACE`（通过接口发送）。
- **同步模式**：当前所有规则均为 `NO_SYNC`（不同步）。
- **布尔开关**：每条规则有 3 个布尔标志位，当前均为 `false`。
- **备注**：仅 `CP-GR-000001`（反洗钱）有备注「反洗钱风险控制」，其余为空。
- **标签**：用于业务分类，取值为 `反洗钱` / `反欺诈` / `数据埋点`。

## 业务分类

- **反洗钱**：`CP-GR-000001 反洗钱`。
- **反欺诈**：
  - `CP-GR-000002 支付事件反欺诈`
  - `CP-GR-000003 非支付事件反欺诈`
- **数据埋点**：
  - `CP-GR-000004 支付事件结果通知`
  - `CP-GR-000005 非支付事件结果通知`

## 行级操作

每条规则在列表右侧提供 3 个操作按钮：

- **修改**：编辑规则基础属性。
- **变量定义**：维护该规则使用的变量。
- **数据分发**：配置数据分发相关项。
