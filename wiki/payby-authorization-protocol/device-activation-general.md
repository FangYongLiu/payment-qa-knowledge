---
title: 设备激活（通用）
domain: payby-authorization-protocol
kind: wiki_page
slug: device-activation-general
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:da01d6e4-7ae2-40ea-84c0-e507fe905e0b
tags: []
---

# 设备激活（通用）

本页介绍后台 TMS 模块中 **Device Approval（设备审批）** 页面的导航位置、筛选条件与申请列表展示。

## 页面入口

位于左侧导航 **TMS** 分组下，菜单项 **Device Approval**。同组其他菜单项包括：

- Device ActiveCode
- Activated Devices
- Device Channel Man...
- Returned Devices
- POS Settings
- Data Tracking
- Amex Mapping
- Operation Logs

左侧一级导航分组：GENERAL、BUSINESS、TMS、SYSTEM、API。

## 筛选区

页面顶部提供搜索栏，支持以下筛选项与操作：

- Merchant ID
- Merchant Name
- Store Name
- 状态下拉框（默认 `ALL`）
- **Search** 按钮

## 申请列表

筛选区下方展示设备审批申请表格，包含以下列：

| 列 | 说明 |
|---|---|
| Apply ID | 申请编号 |
| Merchant ID | 商户号 |
| Merchant Name | 商户名称 |
| Contact Mobile | 联系手机号 |
| Store Name | 门店名称 |
| Device Type | 设备类型 |
| Device Number | 设备数量 |
| Application Time | 申请时间 |
| Status | 审批状态 |
| Action | 操作（View） |

### 设备类型枚举

列表中出现的 `Device Type` 取值示例：

- `VIRTUAL_POS`
- `SMART_POS`
- `BOX`

### 状态与操作

- `Status` 示例值：`Approved`
- `Action` 列提供 **View** 链接，用于查看申请详情。

## 示例记录

| Apply ID | Merchant ID | Merchant Name | Store Name | Device Type | Device Number | Application Time | Status |
|---|---|---|---|---|---|---|---|
| 100773 | 200000430641 | 北京奥金拓网络科技有限公司 | 北京奥金拓分店1 | VIRTUAL_POS | 2 | 2024-12-16 11:25:48 | Approved |
| 100772 | 200000430641 | 北京奥金拓网络科技有限公司 | 北京奥金拓分店1 | SMART_POS | 112 | 2024-12-16 10:42:40 | Approved |
| 100771 | 200000430641 | 北京奥金拓网络科技有限公司 | 北京奥金拓分店1 | BOX | 111 | — | — |

联系手机号统一为 `+86-13565788908`。
