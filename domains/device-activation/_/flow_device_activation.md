---
id: flow_device_activation
object_type: Flow
domain: device-activation
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: confluence:AQ/1135345829
tags:
- Smart POS
- 激活码
- 二维码激活
subdomain: null
module: null
sensitivity: normal
name: 设备激活流程
aliases: []
related_services:
- basis-merchant
related_tables:
- tbl_device_apply_order
- tbl_active_code
- tbl_hardware_info
- tbl_device_key
- tbl_merchant_device
- tbl_device_ext
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 概述
端到端流程：商户控台申请激活码（设备类型 Smart POS）→ basis-merchant 审核 → 审核通过后生成激活二维码 → POS 扫码激活并保存设备及商户关系。

## 步骤(跨系统)
1. 商户控台发起设备激活码申请，选择设备类型 Smart POS。
2. basis-merchant 进行审核（通过 / 驳回）。
   - 申请记录写入 `device.t_device_apply_order`，状态流转：`CREATED` 已创建 → `PASSED` 已通过 / `REJECTED` 已驳回 → `ACTIVE_CODE_CREATED` 激活码已创建。
3. 审核通过后生成设备激活码，写入 `device.t_active_code`，`active_code` 为激活码值，初始状态 `ENABLE` 未使用。
4. 系统基于激活码生成激活二维码。
5. POS 扫码进行激活：
   - 激活码状态由 `ENABLE` 流转为 `USED`。
   - 首次激活保存设备信息到 `device.t_hardware_info`（SN 为物理设备序列号，type 为激活的设备类型）。
   - 保存设备公钥到 `device.t_device_key`，其 `id = t_hardware_info.id`。
   - 保存商户-门店-设备号关系到 `device.t_merchant_device`，`hardware_id = t_hardware_info.id`。
   - 保存设备开通的功能配置到 `device.t_device_ext`，`device_id = t_merchant_device.id`。

## 涉及服务/表
- 服务：basis-merchant（审核）
- 表：
  - [[tbl_device_apply_order]] `device.t_device_apply_order` 设备申请订单表
  - [[tbl_active_code]] `device.t_active_code` 设备激活码表
  - [[tbl_hardware_info]] `device.t_hardware_info` 设备硬件信息表
  - [[tbl_device_key]] `device.t_device_key` 设备公钥表
  - [[tbl_merchant_device]] `device.t_merchant_device` 商户-设备关系表
  - [[tbl_device_ext]] `device.t_device_ext` 设备功能扩展配置表

## 校验点
- `t_device_apply_order.status` 是否按 `CREATED → PASSED → ACTIVE_CODE_CREATED` 正确流转；驳回路径为 `REJECTED`。
- `t_active_code` 是否生成对应记录，`active_code` 有值，状态由 `ENABLE` → `USED`。
- 激活后 `t_hardware_info` 是否写入，SN、type 正确。
- `t_device_key.id` 是否等于 `t_hardware_info.id`。
- `t_merchant_device.hardware_id` 是否等于 `t_hardware_info.id`，商户-门店-设备关系是否正确建立。
- `t_device_ext.device_id` 是否等于 `t_merchant_device.id`，功能配置是否按预期开通。
