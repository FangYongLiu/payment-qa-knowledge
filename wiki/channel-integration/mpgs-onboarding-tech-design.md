---
title: MPGS Onboarding 技术方案
domain: channel-integration
kind: wiki_page
slug: mpgs-onboarding-tech-design
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:4cf298fc-0772-4e55-90a4-e4984464d285
tags: []
---

# MPGS Onboarding 技术方案

本页描述 MPGS 渠道下，商户 / 门店 / 设备登记系统的用例结构与触发事件来源。

## 参与者与触发事件

- **pcenter 发起商户开通产品集事件**（包含 `payChannel`）
- **开通门店事件**
- **绑定设备事件**
- **管理员**（通过 Onboarding Management 页面操作上报）

## 登记系统用例

登记系统包含 4 个入口任务，分别对应不同来源：

- 商户开通产品集的登记任务（来自 pcenter 事件）
- 门店开通的登记任务（来自开通门店事件）
- 绑定设备的登记任务（来自绑定设备事件）
- Onboarding Management 页面操作上报（来自管理员）

## 核心登记用例

中间层的三个核心登记动作：

- 登记商户
- 登记门店
- 登记设备

## 共享子用例

所有核心登记动作共享以下两个子用例：

- 分配号段
- 保存登记结果

## 用例 include 关系

入口任务到核心登记的 «include» 关系：

- 商户开通产品集的登记任务 → **登记商户**
- 门店开通的登记任务 → **登记门店**（上游同时 include 登记商户）
- 绑定设备的登记任务 → **登记设备**（上游同时 include 登记门店 / 登记商户）
- Onboarding Management 页面操作上报 → **登记设备**

核心登记到共享子用例的 «include» 关系：

- 登记商户 → 分配号段、保存登记结果
- 登记门店 → 分配号段、保存登记结果
- 登记设备 → 分配号段、保存登记结果
