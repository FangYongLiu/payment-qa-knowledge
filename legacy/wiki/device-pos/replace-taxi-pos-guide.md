---
title: 出租车POS替换操作指南
domain: device-pos
kind: wiki_page
slug: replace-taxi-pos-guide
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:0dac652a-55d9-460c-b427-e6d05aa28999
tags: []
---

# 出租车POS替换操作指南

通过 BASIS 控台 TMS 模块的 Activated Devices 页面，定位目标已激活设备并进入设备配置，完成出租车 POS 的替换操作。

## 入口路径

- 控台：PAYBY BASIS
- 左侧菜单：TMS → Activated Devices → Activated Devices

## 查找设备

在 Activated Devices 页面顶部筛选区填写条件，点击 `Search` 进行检索。

筛选字段：

- Merchant ID
- Store ID
- Store Name
- Device ID
- 设备类型下拉（出租车 POS 场景选择 `CUSTOMIZED_VPOS`）

## 结果列表

检索结果以表格展示，列包含：

- Merchant ID
- Merchant Name
- Store ID
- Store Name
- Device ID
- Device Type
- Updated Time
- Action

## 执行替换

在目标设备所在行的 `Action` 列，点击 `Device Configuration` 按钮，进入设备配置页面完成 POS 替换。

> 示例记录：Merchant ID `200010278881`、Merchant Name `ADCB`、Device Type `CUSTOMIZED_VPOS`。
