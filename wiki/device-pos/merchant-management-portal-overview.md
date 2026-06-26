---
title: 商户管理与控台模块总览(占位)
domain: device-pos
kind: wiki_page
slug: merchant-management-portal-overview
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/1135345829
tags: []
related_services:
  - svc_basis_merchant
  - svc_device
  - svc_onboarding
related_tables:
  - tbl_active_code
  - tbl_device_apply_order
  - tbl_device_db
  - tbl_hardware_info
  - tbl_merchant_device
---

# 商户管理与控台模块总览(占位)

本页是 Merchant Management & Portal 模块的骨架占位，记录商户接入、配置与控台管理相关的文档框架。当前已补充设备激活码申请与设备激活流程相关内容。

## 文档元信息

- Last updated: 2026-04-13
- Updated by: AI
- 业务域: merchant-management

## 1. Business Flow (业务流程)

- **Overview**: Merchant onboarding, configuration, and portal management operations。当前已覆盖：商户通过控台申请设备激活码并完成 POS 设备激活的流程。
- **Flow Diagram**: 详见 [[flow_device_activation]]
- **Key Business Rules**:
  - 商户在控台发起激活码申请，需选择设备类型（如 Smart POS）。
  - 申请由 `basis-merchant` 进行审核。
  - 审核通过后系统生成激活二维码，使用 POS 扫码完成激活。
  - 设备首次激活时保存硬件信息、设备公钥、商户-门店-设备关系及功能配置。

## 2. System Flow (系统流程)

- **System Architecture**: 表头 Service/App | Role | Database — 待补充（已知 `basis-merchant` 负责激活码申请审核）
- **API Call Chain**: 待补充，参见 [[flow_device_activation]]
- **Key Database Tables**:

| Table | Database | Purpose |
|---|---|---|
| [[tbl_device_apply_order]] `device.t_device_apply_order` | device | 设备申请订单表，状态：`CREATED` 已创建 / `PASSED` 已通过 / `REJECTED` 已驳回 / `ACTIVE_CODE_CREATED` 激活码已创建 |
| [[tbl_active_code]] `device.t_active_code` | device | 设备激活码表，字段 `active_code` 为激活码值；状态：`ENABLE` 未使用 / `USED` 已使用 |
| [[tbl_hardware_info]] `device.t_hardware_info` | device | 设备硬件信息表，设备首次激活后保存；`SN` 为物理设备序列号，`type` 为激活的设备类型 |
| `device.t_device_key` | device | 设备公钥，`id = t_hardware_info.id` |
| [[tbl_merchant_device]] `device.t_merchant_device` | device | 商户-设备关系表，设备激活后保存商户-门店-设备号关系，`hardware_id = t_hardware_info.id` |
| `device.t_device_ext` | device | 设备开通的功能配置，`device_id = t_merchant_device.id` |

## 3. How to Test (测试方法)

- **Test Environment**: 待补充
- **Test Approach**:
  - 通过商户控台发起激活码申请（设备类型选择 Smart POS）。
  - 由 `basis-merchant` 审核（通过 / 驳回）。
  - 审核通过后获取激活二维码，使用 POS 扫码激活。
  - 通过查询 device 库相关表校验各阶段状态流转。
- **Key Test Points**:
  - `t_device_apply_order.status` 流转：`CREATED` → `PASSED` / `REJECTED` → `ACTIVE_CODE_CREATED`。
  - `t_active_code.status` 流转：`ENABLE` → `USED`。
  - 激活后 `t_hardware_info`、`t_device_key`、`t_merchant_device`、`t_device_ext` 数据落库及外键关联正确。

## 4. Test Cases (测试用例)

- **Test Case Summary**: 表头 ID | Title | Priority | Type | Status — 待补充

## 备注

本页持续完善中，已补充设备激活码申请与激活流程相关数据表说明，详细端到端流程见 [[flow_device_activation]]。
