---
id: tbl_device_db
object_type: Table
domain: payment-databases
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: confluence:tester/124289264
tags:
- device
- 硬件
- 激活码
subdomain: device
module: null
sensitivity: normal
name: 设备库(device)核心表
aliases:
- device
related_services: []
related_tables:
- tbl_merchant_db
- tbl_member_db
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
`device` 库用于存储支付终端/设备相关的核心数据，覆盖设备硬件信息、商户与设备的绑定关系、激活码、设备申请流程以及设备密钥管理。

## 关键列
- `device.t_hardware_info`：设备信息表，记录设备硬件信息。
- `device.t_merchant_device`：商户绑定设备表，维护商户与设备的绑定关系。
- `device.t_active_code`：激活码表，记录设备激活码。
- `device.t_device_apply_order`：设备申请列表，记录设备申请订单。
- `device.t_device_key`：设备密钥表，存储设备相关密钥信息。

## 主键/索引
原文未提供主键/索引信息。

## 校验点(QA 关注)
- 设备绑定商户的场景：核对 `t_merchant_device` 与 `merchant.t_merchant` 中商户的对应关系是否正确。
- 激活流程：检查 `t_active_code` 中激活码状态与 `t_device_apply_order` 申请单的状态一致性。
- 硬件信息：核对 `t_hardware_info` 中设备型号/硬件标识与申请、绑定、密钥等数据的一致性。
- 密钥管理：关注 `t_device_key` 是否与设备一一对应，密钥下发是否随设备绑定/激活动作正确生成。
- 与会员设备关联场景，可对照 `member.tr_member_device`、`member.tm_device`，避免会员侧设备信息与商户侧设备信息不一致。
