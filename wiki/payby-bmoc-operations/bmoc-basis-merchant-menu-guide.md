---
title: Basis Merchant 核心菜单功能与权限说明
domain: payby-bmoc-operations
kind: wiki_page
slug: bmoc-basis-merchant-menu-guide
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/1310621839
tags: []
---

# Basis Merchant 核心菜单功能与权限说明

本页聚焦 BMOC 控台中 Basis Merchant 模块的核心菜单路径、用途与操作流程，并给出账号权限管理建议与常见问题速览。模块整体定位与分类参见 [[bmoc-basis-merchant-overview]]。

## 菜单结构总览

Basis Merchant 涉及商户信息配置、产品权限审批、员工/门店/结算设置、POS 设备管理、报表/账单、调账与对账等模块，按功能分类如下：

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

## 商户入驻审核（Onboarding Management）

- **路径**：`/BUSINESS/Merchant/Merchant Onboarding/Onboarding Management`
- **用途**：审批商户提交的注册申请，包括资料校验、资质上传、产品选择等。
- **操作流程**：
  1. 搜索待审核商户
  2. 查看详细资料页
  3. 审核通过 / 驳回 / 修改配置

## 权限说明与账号管理建议

- 登录 BMOC 控台需使用员工域账号（如：`fangyong.liu`）。
- 系统角色与操作权限的配置归属 `Permissions` 菜单，操作记录通过 `Operate Log` 留痕。

## 常见问题

- 控台访问与角色分配相关问题，建议先确认域账号是否已开通，以及对应菜单是否已在 `Permissions` 中授权。
