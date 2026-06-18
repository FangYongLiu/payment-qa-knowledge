---
id: tbl_hardware_info
object_type: Table
domain: device-activation
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: wiki:de4113f2-55a3-48f8-b592-6714684acf4c
tags:
- 设备激活
- 硬件信息
subdomain: null
module: null
sensitivity: normal
name: 设备硬件信息表
aliases:
- t_hardware_info
- device.t_hardware_info
related_services: []
related_tables:
- tbl_active_code
- tbl_merchant_device
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
保存设备首次激活后的物理硬件信息。设备扫描激活二维码完成激活后，向该表写入一条记录，记录设备的物理序列号与激活的设备类型。

## 关键列
- `SN`：物理设备序列号
- `type`：激活的设备类型（本场景为 Smart POS）

## 主键/索引
- `id`：主键，被下列表外键引用：
  - `device.t_device_key.id = t_hardware_info.id`（设备公钥）
  - `device.t_merchant_device.hardware_id = t_hardware_info.id`（商户-设备关系）

## 校验点(QA 关注)
- 设备首次激活成功后，`device.t_hardware_info` 应新增一条记录，且 `SN` 与物理设备序列号一致、`type` 与申请单中的设备类型（Smart POS）一致。
- 同一次激活动作，`t_hardware_info` 的 `id` 应能在 `t_device_key.id` 与 `t_merchant_device.hardware_id` 中关联到对应记录。
- 与 `t_active_code` 联动：激活码状态由 `ENABLE` 变为 `USED` 时，`t_hardware_info` 应同步生成对应硬件记录。
