---
title: Basis Merchant 菜单功能详解
domain: device-pos
kind: wiki_page
slug: bmoc-basis-merchant-menu-guide
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:6d32cc0f-2e65-47ff-95c8-628d0cd82aa4
tags: []
---

# Basis Merchant 菜单功能详解

本页梳理 BMOC 控台中 Basis Merchant 模块下的菜单分类、典型路径与核心菜单(如商户入驻审核)的用途与操作流程,并给出账号权限管理建议与常见问题速览,便于测试、产品、运营快速定位功能入口。模块整体定位与分类参见 [[bmoc-basis-merchant-overview]]。

## 适用范围

- **目的**:帮助使用者掌握 Basis Merchant 各菜单的路径、作用与操作要点。
- **适用人群**:测试人员、产品经理、开发、运营。
- **覆盖能力**:商户信息配置、产品权限审批、员工/门店/结算设置、POS 设备管理、报表/账单、调账与对账等。

## 控台入口与界面结构

- **控台名称**:PayBy Basis(顶部标识 `PAYBY BASIS` / `WELCOME TO PAYBY`)。
- **顶部工具栏**:语言切换、消息通知、全屏、当前登录用户信息。
- **左侧主导航**:
  - `GENERAL`
  - `BUSINESS`(Basis Merchant 主要功能所在分组)
    - `Merchant`(展开后包含商户相关子菜单)
  - `TMS`(POS 终端与设备管理)

## 菜单结构总览(按模块分类)

Basis Merchant 涉及商户信息配置、产品权限审批、员工/门店/结算设置、POS 设备管理、报表/账单、调账与对账等模块,按功能分类如下:

| 功能分类 | 主要菜单项(路径) | 简要说明 |
|---|---|---|
| 📌 商户管理 | Merchant Management | 查询/编辑商户资料、设置结算信息等 |
| 📌 商户入驻与开通 | Merchant Approval、Application Approval、Onboarding Management、Open Product | 商户开户/申请审核、产品申请流程 |
| 📌 税务相关 | Tax Info Approval、Tax Invoice | 商户税务信息审核、税务发票管理 |
| 📌 员工门店管理 | Staff Management、Store Management、Cashier Management、Member Config | 配置门店、员工、收银员等 |
| 📌 渠道配置 | Fund Provider Management、3rd Party MID | 管理商户绑定的收单通道、上送渠道信息 |
| 📌 设备管理 | TMS > Device Approval / Activated Devices | 审批 POS、查看终端状态 |
| 📌 报表与对账 | Statements、Reconciliation、Reconciliation Summary / Clear Flow / Fund Flow | 结算账单查看、对账、异常调账 |
| 📌 银行账户 | Bank Account Approval | 商户银行账户变更审核 |
| 📌 安全与解绑 | Staff 2FA Unbind | 员工二次验证解绑 |
| 📌 权限与日志 | Permissions、Operate Log | 操作日志查看、系统角色配置 |
| 📌 公告 | Announcements | 控台通知与公告管理 |

## 核心菜单:商户入驻审核

Basis Merchant 中商户审核入口包含 `Merchant Approval`(BUSINESS > Merchant 下)与 `Onboarding Management`,二者均用于商户注册/入驻申请的审批,使用方根据控台版本选择对应入口。

### Merchant Approval

- **路径**:`BUSINESS > Merchant > Merchant Approval`
- **用途**:审批商户提交的注册申请,涵盖代理商(AGENT)与商户自助(PORTAL)等多个来源。
- **筛选条件**:
  - `Merchant ID`、`Agent Mid`、`Merchant Name`、`Contact Mobile`
  - 状态下拉(`ALL`)、类型下拉(`All Type`)、来源下拉(`All Source`)
  - `Search` 查询按钮、`+ New Merchant` 新建商户按钮
- **列表字段**:`Apply ID`、`Source`、`Merchant ID`、`Merchant Name`、`Contact Mobile`、`Application Time`、`Status`、`Action`
- **常见状态**:`Awaiting Approval`(待审核)等。
- **行操作**:`View`(查看)、`Approval`(审核)、`Add Staff`(添加员工)。
- **来源类型(Source)**:
  - `AGENT`:由代理商代为提交
  - `PORTAL`:商户通过自助门户提交

### Onboarding Management

- **路径**:`/BUSINESS/Merchant/Merchant Onboarding/Onboarding Management`
- **用途**:审批商户提交的注册申请,覆盖资料校验、资质上传、产品选择等环节。
- **操作流程**:
  1. 搜索待审核商户
  2. 查看详细资料页
  3. 执行审核通过 / 驳回 / 修改配置

## 权限说明与账号管理建议

- 登录 BMOC 控台需使用员工域账号(如:`fangyong.liu`、`Can Wang`)。
- 系统角色与操作权限的配置归属 `Permissions` 菜单,操作记录通过 `Operate Log` 留痕。
- 涉及员工二次验证异常时,可通过 `Staff 2FA Unbind` 菜单进行解绑处理。

## 常见问题

- 控台访问与角色分配相关问题,建议先确认域账号是否已开通,以及对应菜单是否已在 `Permissions` 中授权。
- 在 `Merchant Approval` 列表看不到目标申请时,优先确认筛选条件中的 `Source`(AGENT/PORTAL)与状态过滤是否正确。

## 相关阅读

- 控台账号与登录方式、常见问题处理见 [[bmoc-access-and-faq]]。
