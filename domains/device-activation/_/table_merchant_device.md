---
id: tbl_merchant_device
object_type: Table
domain: device-activation
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: confluence:AQ/1135345829
tags:
- device
- merchant
subdomain: null
module: null
sensitivity: normal
name: 商户-设备关系表
aliases:
- t_merchant_device
related_services: []
related_tables:
- tbl_hardware_info
- tbl_device_ext
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
设备激活后保存商户-门店-设备号关系。库表：`device.t_merchant_device`。

## 关键列
- `id`：主键，被 `t_device_ext.device_id` 引用。
- `hardware_id`：关联 `t_hardware_info.id`。

## 主键/索引
- 主键：`id`。
- 外部引用：`hardware_id` → `t_hardware_info.id`；`t_device_ext.device_id` → 本表 `id`。

## 校验点(QA 关注)
- 设备激活成功后，本表应生成商户-门店-设备号关联记录。
- `hardware_id` 必须能在 `t_hardware_info` 中找到对应记录（设备首次激活时写入硬件信息）。
- 与 `t_device_ext` 的关联：`t_device_ext.device_id` 应等于本表 `id`，确认设备开通的功能配置挂在正确的商户-设备关系上。
