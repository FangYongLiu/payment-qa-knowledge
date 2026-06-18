---
title: PayBy商户控台(Merchant Portal)总览
domain: payby-authorization-protocol
kind: wiki_page
slug: payby-merchant-portal-overview
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:d0fc9a05-973a-470e-8b1c-3f41e297dd33
tags: []
---

# PayBy商户控台(Merchant Portal)总览

PayBy Merchant Portal（商户控台，标题区显示为 "PAYBY BASIS"）是一个面向商户/运营的后台管理 Web UI，用于商户、设备、系统等多模块的管理操作。登录后顶部显示 "WELCOME TO PAYBY"，并提供折叠与刷新按钮。

## 导航结构

左侧侧边栏按功能域分组，主要包含：

- **GENERAL**
- **BUSINESS**
- **TMS**（终端管理系统，可展开）
- **SYSTEM**

### TMS 模块子项

- Device Approval（设备审批）
- Device ActiveCode（设备激活码）
- Activated Devices（已激活设备，可展开）
- Device Channel Management（设备渠道管理）
- Returned Devices（退回设备）
- POS Settings（POS 设置）
- Data Tracking（数据追踪）
- Amex Mapping（Amex 映射）
- Operation Logs（操作日志）

## Device Approval 页面

进入 TMS → Device Approval，主面板标题为 "Device Approval"，用于对商户提交的设备申请进行审批查看。

### 筛选条件

页面顶部提供以下筛选输入与一个 Search 按钮：

- Merchant ID（文本输入）
- Merchant Name（文本输入）
- Store Name（文本输入）
- 状态下拉框（默认 `ALL`）
- Search 按钮（带放大镜图标）

### 申请列表字段

数据表支持按列排序，列包括：

| 字段 | 说明 |
|---|---|
| Apply ID | 申请单号 |
| Merchant ID | 商户号 |
| Merchant Name | 商户名称 |
| Contact Mobile | 联系电话 |
| Store Name | 门店名称 |
| Device Type | 设备类型（如 `SMART_POS`、`BOX`） |
| Device Number | 设备数量 |

示例数据（节选）：

- `100785` / `200000430854` / 北京青子未来网络科技有限… / `+86-19545952191` / 青子分店1 / `SMART_POS` / 5
- `100784` / `200000030906` / regress6666 / `+971-585920614` / Asdaa Street / `BOX` / 3
- `100783` / `200000430854` / 北京青子未来网络科技有限… / `+86-19545952191` / 青子分店1 / `SMART_POS` / 5

> Device Type 已观察到的枚举值：`SMART_POS`、`BOX`。
