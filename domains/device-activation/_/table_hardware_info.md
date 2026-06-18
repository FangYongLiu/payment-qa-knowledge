---
id: tbl_hardware_info
object_type: Table
domain: device-activation
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: confluence:AQ/1135345829
tags:
- 设备信息
- SN
- 硬件
subdomain: null
module: null
sensitivity: normal
name: 设备硬件信息表
aliases:
- t_hardware_info
related_services: []
related_tables:
- tbl_device_key
- tbl_merchant_device
related_scenarios:
- flow_device_activation
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
设备首次激活后保存设备信息，记录物理设备的硬件标识与激活类型。表名：`device.t_hardware_info`。

## 关键列
- `SN`：物理设备序列号
- `type`：激活的设备类型（如 Smart POS）
- `id`：设备硬件信息主键，被 `t_device_key.id` 与 `t_merchant_device.hardware_id` 引用

## 主键/索引
- 主键：`id`（被 `t_device_key.id`、`t_merchant_device.hardware_id` 关联）

## 校验点(QA 关注)
- 设备首次激活后是否成功落库 `t_hardware_info`
- `SN` 是否与物理设备序列号一致
- `type` 是否与申请激活码时的设备类型（Smart POS）一致
- 关联校验：`t_device_key.id = t_hardware_info.id`；`t_merchant_device.hardware_id = t_hardware_info.id`
