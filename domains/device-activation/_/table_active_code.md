---
id: tbl_active_code
object_type: Table
domain: device-activation
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: wiki:de4113f2-55a3-48f8-b592-6714684acf4c
tags:
- 激活码
- 状态
subdomain: null
module: null
sensitivity: normal
name: 设备激活码表
aliases:
- t_active_code
related_services: []
related_tables:
- tbl_device_apply_order
- tbl_hardware_info
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
存储设备激活码值及其使用状态。设备申请订单审核通过(`t_device_apply_order` 状态变为 `ACTIVE_CODE_CREATED`)后，会在该表生成激活码记录，用于生成激活二维码供 Smart POS 扫码激活。

## 关键列
- `active_code`：激活码值
- 状态：
  - `ENABLE`：未使用
  - `USED`：已使用

## 主键/索引
原文未提供。

## 校验点(QA 关注)
- 申请订单审核通过后，`device.t_active_code` 应生成对应记录，初始状态为 `ENABLE`
- POS 扫码激活成功后，对应激活码状态应由 `ENABLE` 变为 `USED`
- 激活码状态流转应与 `t_device_apply_order.ACTIVE_CODE_CREATED` 状态一致
