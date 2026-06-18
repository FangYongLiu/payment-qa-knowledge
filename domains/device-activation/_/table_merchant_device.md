---
id: tbl_merchant_device
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
- 商户绑定
subdomain: null
module: device
sensitivity: normal
name: 商户设备关系表
aliases:
- t_merchant_device
related_services: []
related_tables:
- tbl_hardware_info
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
设备激活后，保存商户-门店-设备号的绑定关系。维护设备与所属商户/门店之间的归属信息，作为设备激活落地后的核心关系表。

## 关键列
- `hardware_id`：关联 `t_hardware_info.id`，指向具体的物理设备硬件信息记录
- 商户、门店、设备号相关字段：用于表达"商户-门店-设备"的三元绑定关系（原文未列出具体列名）

## 主键/索引
- 主键 `id`：被 `t_device_ext.device_id` 引用（`device_id = t_merchant_device.id`），用于挂载设备开通的功能配置

## 校验点(QA 关注)
- 设备激活成功后，应在 `device.t_merchant_device` 中产生对应记录，且 `hardware_id` 与 `t_hardware_info.id` 一致
- 商户-门店-设备号关系应与申请阶段（`t_device_apply_order`）中商户/门店信息一致
- 关联检查：通过 `t_merchant_device.id` 应能在 `t_device_ext` 中查询到设备功能配置
- 同一物理设备（同 `hardware_id`）的绑定关系应符合业务唯一性约束（避免重复绑定）
