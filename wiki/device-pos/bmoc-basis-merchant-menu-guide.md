---
title: Basis Merchant 菜单功能详解
domain: device-pos
kind: wiki_page
slug: bmoc-basis-merchant-menu-guide
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:be47e704-2647-4e66-b727-b8ffd09c1e8a
tags: []
---

# Basis Merchant 菜单功能详解

本页梳理 BMOC 控台中 Basis Merchant 模块下的菜单分类、典型路径与核心菜单(如商户入驻审核、设备激活码)的用途与操作流程,并给出账号权限管理建议与常见问题速览,便于测试、产品、运营快速定位功能入口。

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
| 📌 设备管理 (TMS) | Device Approval、Device ActiveCode、Activated Devices、Devices Channel Mapping、POS Settings、Amex Mapping、Operation Logs | 审批 POS、生成激活码、查看终端状态、通道映射、POS 配置等 |
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

## 核心菜单:TMS 设备管理

TMS 模块用于管理 POS 终端的全生命周期,主要子菜单包括:

- **Device Approval**:审批新提交的设备申请。
- **Device ActiveCode**:为商户/门店生成并查看设备激活二维码。
- **Activated Devices**:已激活终端列表(含 Fiserv Outbound、Fiserv Exception 等子项)。
- **Devices Channel Mapping**:设备与收单通道的映射关系。
- **POS Settings**:POS 终端参数配置。
- **Amex Mapping**:Amex 渠道映射配置。
- **Operation Logs**:TMS 模块操作日志。

### Device ActiveCode

- **用途**:按商户维度查询并下发设备激活码(QR Code),供 POS 设备扫码激活。
- **查询条件**:`Merchant ID`(顶部搜索框)。
- **列表字段**:`No.`、`Merchant Mid`、`Device Type`、`Store Name`、`Store Location`、`QR Code`。
- **操作要点**:
  1. 输入 `Merchant ID` 点击 `Search` 过滤目标商户。
  2. 在结果行中查看对应门店(如 `ADCB Store`、`Cars Taxi L.L.C Abu Dhabi office`)的二维码。
  3. 将 QR Code 提供给现场人员供 POS 扫码激活。

## 权限说明与账号管理建议

- 登录 BMOC 控台需使用员工域账号(如:`fangyong.liu`、`Can Wang`)。
- 系统角色与操作权限的配置归属 `Permissions` 菜单,操作记录通过 `Operate Log` 留痕;TMS 内的具体设备操作另有 `Operation Logs` 子菜单留痕。

## 常见问题

- 控台访问与角色分配相关问题,建议先确认域账号是否已开通,以及对应菜单(尤其是 TMS 子项)是否已在 `Permissions` 中授权。
- 在 `Device ActiveCode` 列表中若 `Device Type` / `Store Location` 为空,通常是商户侧资料未补齐,需回到 Merchant Management 完善门店信息。
