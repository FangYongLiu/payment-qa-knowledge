---
title: Basis Merchant 菜单功能详解
domain: merchant-management
kind: wiki_page
slug: bmoc-basis-merchant-menu-guide
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:d3d9d62f-6df4-4669-aeab-f63d6dad3420
tags: []
---

# Basis Merchant 菜单功能详解

本页梳理 BMOC 控台中 Basis Merchant 模块下的菜单分类、典型路径与核心菜单(如商户入驻审核)的用途与操作流程,并给出账号权限管理建议与常见问题速览,便于测试、产品、运营快速定位功能入口。模块整体定位与分类参见 [[bmoc-basis-merchant-overview]]。

## 适用范围

- **目的**:帮助使用者掌握 Basis Merchant 各菜单的路径、作用与操作要点。
- **适用人群**:测试人员、产品经理、开发、运营。
- **覆盖能力**:商户信息配置、产品权限审批、员工/门店/结算设置、POS 设备管理、报表/账单、调账与对账等。

## 控台入口

- 控台名称:**PAYBY BASIS**(顶部标识 "WELCOME TO PAYBY")。
- 顶部工具区包含:语言切换、外链、通知、全屏与当前登录用户头像(示例:`Can Wang`)。
- 左侧主导航分为 **GENERAL**、**BUSINESS**、**TMS** 等一级模块,Basis Merchant 相关菜单位于 `BUSINESS > Merchant` 下。

## 菜单结构总览(按模块分类)

Basis Merchant 涉及商户信息配置、产品权限审批、员工/门店/结算设置、POS 设备管理、报表/账单、调账与对账等模块,按功能分类如下:

| 功能分类 | 主要菜单项(路径) | 简要说明 |
|---|---|---|
| 📌 商户管理 | Merchant Management | 查询/编辑商户资料、设置结算信息等 |
| 📌 商户入驻与开通 | Onboarding Management、Open Product、Merchant Approval、Application Approval | 商户开户审核、产品申请流程 |
| 📌 渠道配置 | Fund Provider Management、3rd Party MID | 管理商户绑定的收单通道、上送渠道信息 |
| 📌 设备管理 | TMS > Device Approval / Activated Devices | 审批 POS、查看终端状态 |
| 📌 员工门店管理 | Member Config、Store Management、Staff Management、Cashier Management | 配置门店信息、员工与收银员权限等 |
| 📌 报表与对账 | Statements、Reconciliation、Reconciliation Summary / Clear Flow / Fund Flow | 结算账单查看、异常调账 |
| 📌 权限与日志 | Permissions、Operate Log、Staff 2FA Unbind | 操作日志查看、系统角色配置、员工 2FA 解绑 |
| 📌 税务与公告 | Tax Invoice、Tax Info Approval、Announcements | 税务信息审批、税务报表生成与控台通知 |
| 📌 银行账户 | Bank Account Approval | 商户银行账户信息审核 |

### BUSINESS > Merchant 子菜单速查

控台左侧 `BUSINESS > Merchant` 展开后包含以下子项:

- Merchant Approval
- Application Approval
- Tax Info Approval
- Staff Management
- Store Management
- Cashier Management
- Reconciliation
- Statements
- Staff 2FA Unbind
- Tax Invoice
- Announcements
- Bank Account Approval

## 核心菜单:商户入驻审核

### Onboarding Management

- **路径**:`/BUSINESS/Merchant/Merchant Onboarding/Onboarding Management`
- **用途**:审批商户提交的注册申请,覆盖资料校验、资质上传、产品选择等环节。
- **操作流程**:
  1. 搜索待审核商户
  2. 查看详细资料页
  3. 执行审核通过 / 驳回 / 修改配置

### Merchant Approval

- **入口**:`BUSINESS > Merchant > Merchant Approval`
- **用途**:对入驻申请进行集中查询、审核与新增,是 PAYBY BASIS 控台中商户审批的主要工作页。
- **筛选条件**(顶部搜索栏,从左到右):
  - Merchant ID
  - Agent Mid
  - Merchant Name
  - Contact Mobile
  - 状态下拉(默认 `ALL`)
  - 类型下拉(默认 `All Type`)
  - 来源下拉(默认 `All Source`)
  - `Search` 按钮、`+ New Merchant` 按钮(用于手工新增商户)
- **列表字段**(支持排序):
  - `Apply ID`:申请单号
  - `Source`:来源,常见值如 `AGENT`、`PORTAL`
  - `Merchant ID`:商户号
  - `Merchant Name`:商户名称
  - `Contact Mobile`:联系手机号
  - `Application Time`:申请时间
  - `Status`:申请状态,如 `Awaiting Approval`(待审核)
  - `Action`:行内操作,包含 `View`、`Approval`、`Add Staff`
- **典型示例**:
  - Apply ID `3380`,Source `AGENT`,Merchant ID `200015065197`,商户 `Tipsme Computer Software Trading`,Status `Awaiting Approval`。
  - Apply ID `3379`,Source `PORTAL`,Merchant ID `200015064424`,商户 `Vasun impex FZ LLC`。
- **操作要点**:
  1. 通过筛选定位待办申请(如按 Source 区分代理商提交与商户门户自助提交)。
  2. 点击 `View` 查看资料详情;点击 `Approval` 进入审核动作页。
  3. 审核通过后可通过 `Add Staff` 直接为该商户补录员工信息。

## 权限说明与账号管理建议

- 登录 BMOC / PAYBY BASIS 控台需使用员工域账号(如:`fangyong.liu`)。
- 系统角色与操作权限的配置归属 `Permissions` 菜单,操作记录通过 `Operate Log` 留痕。
- 员工 2FA 异常时,可通过 `Staff 2FA Unbind` 菜单解绑后重新绑定。

## 常见问题

- 控台访问与角色分配相关问题,建议先确认域账号是否已开通,以及对应菜单是否已在 `Permissions` 中授权。
- 看不到 `Merchant Approval` 等子菜单时,优先检查 `BUSINESS > Merchant` 一级模块是否被授权展开。

## 相关阅读

- 控台账号与登录方式、常见问题处理见 [[bmoc-access-and-faq]]。
