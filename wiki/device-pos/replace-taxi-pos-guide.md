---
title: Taxi POS 替换操作指南
domain: device-pos
kind: wiki_page
slug: replace-taxi-pos-guide
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:25719fa3-7575-4563-8578-ad4e3e540f4f
tags: []
---

# Taxi POS 替换操作指南

本页说明 Taxi POS 设备替换过程中 **Device menu settings** 的配置方法，包括各子菜单的激活操作与 POS 端显示开关。

## Device menu settings 表结构

设备菜单设置页以表格形式展示，包含以下列：

- **Menu Name**：主菜单名称
- **Sub-menu**：子菜单名称
- **Function Status**：功能状态（Active / Inactive）
- **Action**：操作按钮（仅 Inactive 状态显示 `Activate` 按钮）
- **Display on POS**：POS 端显示开关（toggle）

## 菜单与子菜单清单

### Purchase

`Purchase` 主菜单包含多个子菜单（合并单元格展示）：

| Sub-menu | Function Status | Display on POS |
|---|---|---|
| -- | Active | ON |
| PayBy/BOTIM | Active | ON |
| ADCB-NI | Inactive | OFF |
| Tips-Tier1 | Inactive | OFF |
| Tips-Tier2 | Inactive | OFF |
| DCC | Inactive | OFF |
| ADCB-FISERV | Inactive | OFF |
| KLIP | Inactive | OFF |

### Void

- 子菜单 `--`，状态 Active，Display on POS：ON

### Refund

- 子菜单 `--`，状态 Active，Display on POS：OFF

> 注：Refund 虽为 Active，但 POS 端显示开关默认关闭，需根据业务需要单独打开。

## 激活与显示规则

- **Active** 子菜单：Action 列无按钮，Display on POS 默认绿色（ON）。
- **Inactive** 子菜单：Action 列显示蓝色 `Activate` 按钮，Display on POS 为灰色（OFF）。
- 替换 POS 时需根据业务需求点击 `Activate` 激活对应子菜单，并确认 Display on POS 开关状态。

## 替换操作重点

在 Taxi POS 替换流程中，需特别确认以下两个子菜单的激活情况（原文中以红框标注）：

- `Purchase → Tips-Tier1`
- `Purchase → ADCB-FISERV`

激活后请同步检查 Display on POS toggle 是否打开，确保 POS 端能够正常展示对应功能入口。
