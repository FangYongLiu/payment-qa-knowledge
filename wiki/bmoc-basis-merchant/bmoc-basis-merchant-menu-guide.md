---
title: Basis Merchant 菜单功能详解
domain: merchant-portal
kind: wiki_page
slug: bmoc-basis-merchant-menu-guide
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:e02c9096-b59f-4d21-bec7-6a03463d0dfe
tags: []
---

# Basis Merchant 菜单功能详解

本页梳理 BMOC 控台中 Basis Merchant 模块下的菜单分类、典型路径与核心菜单(如商户入驻审核)的用途与操作流程,并给出账号权限管理建议与常见问题速览,便于测试、产品、运营快速定位功能入口。模块整体定位与分类参见 [[bmoc-basis-merchant-overview]]。

## 适用范围

- **目的**:帮助使用者掌握 Basis Merchant 各菜单的路径、作用与操作要点。
- **适用人群**:测试人员、产品经理、开发、运营。
- **覆盖能力**:商户信息配置、产品权限审批、员工/门店/结算设置、POS 设备管理、报表/账单、调账与对账等。

## 菜单结构总览(按模块分类)

Basis Merchant 涉及商户信息配置、产品权限审批、员工/门店/结算设置、POS 设备管理、报表/账单、调账与对账等模块,按功能分类如下:

| 功能分类 | 主要菜单项(路径) | 简要说明 |
|---|---|---|
| 📌 商户管理 | Merchant Management | 查询/编辑商户资料、设置结算信息等 |
| 📌 商户入驻与开通 | Onboarding Management、Open Product | 商户开户审核、产品申请流程 |
| 📌 渠道配置 | Fund Provider Management、3rd Party MID | 管理商户绑定的收单通道、上送渠道信息 |
| 📌 设备管理 | TMS > Device Approval / Activated Devices | 审批 POS、查看终端状态 |
| 📌 员工门店管理 | Member Config、Store、Staff 等 | 配置门店信息、员工权限等 |
| 📌 报表与对账 | Statements、Reconciliation Summary / Clear Flow / Fund Flow | 结算账单查看、异常调账 |
| 📌 权限与日志 | Permissions、Operate Log | 操作日志查看、系统角色配置 |
| 📌 税务与公告 | Tax Invoice、Announcements | 税务报表生成与控台通知 |

## 核心菜单:商户入驻审核(Onboarding Management)

- **路径**:`/BUSINESS/Merchant/Merchant Onboarding/Onboarding Management`
- **用途**:审批商户提交的注册申请,覆盖资料校验、资质上传、产品选择等环节。
- **操作流程**:
  1. 搜索待审核商户
  2. 查看详细资料页
  3. 执行审核通过 / 驳回 / 修改配置

## 权限说明与账号管理建议

- 登录 BMOC 控台需使用员工域账号(如:`fangyong.liu`)。
- 系统角色与操作权限的配置归属 `Permissions` 菜单,操作记录通过 `Operate Log` 留痕。

## 常见问题

- 控台访问与角色分配相关问题,建议先确认域账号是否已开通,以及对应菜单是否已在 `Permissions` 中授权。

## 相关阅读

- 控台账号与登录方式、常见问题处理见 [[bmoc-access-and-faq]]。
