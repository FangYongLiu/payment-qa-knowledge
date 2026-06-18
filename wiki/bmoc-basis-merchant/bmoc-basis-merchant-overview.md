---
title: BMOC Basis Merchant 模块总览
domain: bmoc-basis-merchant
kind: wiki_page
slug: bmoc-basis-merchant-overview
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:e02c9096-b59f-4d21-bec7-6a03463d0dfe
tags: []
---

# BMOC Basis Merchant 模块总览

本页介绍 PayBy 内部 BMOC 控台的定位，以及 Basis Merchant 系统下的菜单分类与核心功能模块概览，帮助测试、产品、运营、开发同学快速建立模块全景认知。

## BMOC 控台介绍

- **BMOC**（Botim Money Operation Console）是 PayBy 内部用于**运营管理**的后台系统。
- **Basis Merchant** 是 BMOC 中聚焦商户运营的系统，覆盖商户信息配置、产品权限审批、员工/门店/结算设置、POS 设备管理、报表/账单、调账与对账等能力。

## 适用人群

- 测试人员
- 产品经理
- 开发
- 运营同事

## Basis Merchant 菜单分类总览

| 功能分类 | 主要菜单项（路径） | 简要说明 |
| --- | --- | --- |
| 📌 商户管理 | Merchant Management | 查询/编辑商户资料、设置结算信息等 |
| 📌 商户入驻与开通 | Onboarding Management, Open Product | 商户开户审核、产品申请流程 |
| 📌 渠道配置 | Fund Provider Management, 3rd Party MID | 管理商户绑定的收单通道、上送渠道信息 |
| 📌 设备管理 | TMS > Device Approval / Activated Devices | 审批 POS、查看终端状态 |
| 📌 员工门店管理 | Member Config, Store, Staff 等 | 配置门店信息、员工权限等 |
| 📌 报表与对账 | Statements, Reconciliation Summary / Clear Flow / Fund Flow | 结算账单查看、异常调账 |
| 📌 权限与日志 | Permissions, Operate Log | 操作日志查看、系统角色配置 |
| 📌 税务与公告 | Tax Invoice, Announcements | 税务报表生成与控台通知 |

## 核心菜单速览

Basis Merchant 的核心入口围绕**商户全生命周期**展开：

- **商户入驻审核**（Onboarding Management）：审批商户注册申请，含资料校验、资质上传、产品选择。
  - 路径：`/BUSINESS/Merchant/Merchant Onboarding/Onboarding Management`
  - 操作流程：搜索待审核商户 → 查看详细资料页 → 审核通过 / 驳回 / 修改配置
- 其他菜单（产品开通、渠道配置、设备审批、门店员工、报表对账、税务公告等）的字段、操作要点详见 [[bmoc-basis-merchant-menu-guide]]。

## 权限与账号

- 登录 BMOC 控台需使用员工域账号（如：`fangyong.liu`）。
- 角色权限、操作日志及登录相关问题参见 [[bmoc-access-and-faq]]。
