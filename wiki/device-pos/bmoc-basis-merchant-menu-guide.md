---
title: Basis Merchant 菜单功能详解
domain: device-pos
kind: wiki_page
slug: bmoc-basis-merchant-menu-guide
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:9ed7df10-1da7-4dcd-bf36-68c2f497d9eb
tags: []
---

# Basis Merchant 菜单功能详解

本页梳理 BMOC 控台中 Basis Merchant 模块下的菜单分类、典型路径与核心菜单(如商户入驻审核、设备管理)的用途与操作流程,并给出账号权限管理建议与常见问题速览,便于测试、产品、运营快速定位功能入口。模块整体定位与分类参见 [[bmoc-basis-merchant-overview]]。

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
| 📌 设备管理 | TMS > Device Approval / Device ActiveCode / Activated Devices / Devices Channel Ma... / POS Settings / Amex Mapping / Operation Logs | 审批 POS、激活码管理、查看终端状态、渠道映射、POS 设置等 |
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

## 核心菜单:设备管理(TMS)

TMS 模块用于管理 POS 终端的全生命周期,左侧导航位于 `TMS` 下,主要子菜单包括:

- **Device Approval**:POS 设备入网审批。
- **Device ActiveCode**:设备激活码管理。
- **Activated Devices**:已激活设备列表与详情维护,含子页 `Fiserv Outbound...`、`Activated Devices`、`Fiserv Exception...`。
- **Devices Channel Ma...**:设备与收单渠道的映射管理。
- **POS Settings**:POS 全局/默认参数配置。
- **Amex Mapping**:Amex 渠道映射配置。
- **Operation Logs**:设备相关操作日志。

### Activated Devices 详情页

进入某台已激活设备的详情后,页面包含以下分区:

- **Device Information**:展示 `Device Type`(如 `SMART_POS`)、`Device ID`(如 `9742`)等基础信息。
- **Printed receipts**:用于配置回单上展示的内容,可通过 `Edit` 按钮编辑;关键字段如 `POS Merchant Name`(例:`APLUS Test Merchant`)。
- **Device menu settings**:配置 POS 端可见菜单项,表格列为:
  - `Menu Name` | `Sub-menu` | `Function Status` | `Action` | `Display on POS`

  以 `Purchase` 主菜单为例,典型子菜单与状态如下:

  | Sub-menu | Function Status | Action | Display on POS |
  |---|---|---|---|
  | -- | Active | -- | ON |
  | PayBy/BOTIM | Active | -- | ON |
  | ADCB-NI | Inactive | Activate | OFF |
  | Tips-Tier1 | Active | Maximum tip amount / Deactivate | OFF |
  | Tips-Tier2 | Inactive | Activate | OFF |
  | DCC | Inactive | Activate | OFF |
  | ADCB-FISERV | Inactive | Activate | -- |

  说明:
  - `Function Status` 表示该子功能是否已启用;`Inactive` 项可通过 `Activate` 按钮申请开通(对应弹窗 `Request activation channels`)。
  - `Display on POS` 控制该菜单是否在 POS 端展示,与 `Function Status` 解耦,可独立切换。
  - `Tips-Tier1` 等小费菜单支持配置 `Maximum tip amount`。

## 权限说明与账号管理建议

- 登录 BMOC 控台需使用员工域账号(如:`fangyong.liu`、`Can Wang`)。
- 系统角色与操作权限的配置归属 `Permissions` 菜单,操作记录通过 `Operate Log` 留痕;TMS 内的设备操作另有 `Operation Logs` 子菜单。

## 常见问题

- 控台访问与角色分配相关问题,建议先确认域账号是否已开通,以及对应菜单是否已在 `Permissions` 中授权。
- POS 端看不到某菜单项时,先检查 `Activated Devices` 详情页中 `Device menu settings` 的 `Function Status` 与 `Display on POS` 是否均已开启。

## 相关阅读

- 控台账号与登录方式、常见问题处理见 [[bmoc-access-and-faq]]。
