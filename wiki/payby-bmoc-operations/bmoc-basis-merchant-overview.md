---
title: BMOC Basis Merchant 模块总览
domain: payby-bmoc-operations
kind: wiki_page
slug: bmoc-basis-merchant-overview
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/1310621839
tags: []
---

# BMOC Basis Merchant 模块总览

本页介绍 BMOC 控台的定位，以及 Basis Merchant 模块的菜单分类与整体结构，帮助测试/运营/产品快速建立全局认知。

## BMOC 控台介绍

- **BMOC**：Botim Money Operation Console，PayBy 内部用于**运营管理**的后台系统。
- **Basis Merchant 系统**覆盖以下能力：
  - 商户信息配置
  - 产品权限审批
  - 员工 / 门店 / 结算设置
  - POS 设备管理
  - 报表 / 账单
  - 调账与对账

## 适用人群与文档目的

- **目的**：帮助使用者快速理解 Basis Merchant 模块下各菜单功能，掌握商户相关审批、配置、设备等操作路径与作用。
- **适用人群**：测试人员、产品经理、开发、运营同事。

## Basis Merchant 菜单结构总览

模块按功能划分为以下 8 大分类：

| 功能分类 | 主要菜单项（路径） | 简要说明 |
|---|---|---|
| 📌 商户管理 | Merchant Management | 查询/编辑商户资料、设置结算信息等 |
| 📌 商户入驻与开通 | Onboarding Management, Open Product | 商户开户审核、产品申请流程 |
| 📌 渠道配置 | Fund Provider Management, 3rd Party MID | 管理商户绑定的收单通道、上送渠道信息 |
| 📌 设备管理 | TMS > Device Approval / Activated Devices | 审批 POS、查看终端状态 |
| 📌 员工门店管理 | Member Config, Store, Staff 等 | 配置门店信息、员工权限等 |
| 📌 报表与对账 | Statements, Reconciliation Summary / Clear Flow / Fund Flow | 结算账单查看、异常调账 |
| 📌 权限与日志 | Permissions, Operate Log | 操作日志查看、系统角色配置 |
| 📌 税务与公告 | Tax Invoice, Announcements | 税务报表生成与控台通知 |

## 登录与账号

- 登录 BMOC 控台需使用**员工域账号**（示例：`fangyong.liu`）。

## 相关页面

- 各菜单的具体功能、操作流程与权限要求详见 [[bmoc-basis-merchant-menu-guide]]。
