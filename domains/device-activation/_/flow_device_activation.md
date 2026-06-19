---
id: flow_device_activation
object_type: Flow
domain: device-pos
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: wiki:de4113f2-55a3-48f8-b592-6714684acf4c
tags: []
subdomain: null
module: null
sensitivity: normal
name: 设备激活端到端流程
aliases: []
related_services: []
related_tables:
- tbl_device_apply_order
- tbl_active_code
- tbl_hardware_info
- tbl_merchant_device
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 概述
Smart POS 设备激活的端到端流程：从商户控台发起激活码申请，经 basis-merchant 审核，生成激活二维码，再由 POS 扫码完成激活并落地商户-设备关系。详见 [[device-activation-overview]]。

## 步骤(跨系统)
1. 商户在控台申请激活码，设备类型选择 Smart POS。
2. basis-merchant 进行审核：
   - 申请记录写入 `device.t_device_apply_order`（[[tbl_device_apply_order]]），状态流转：`CREATED` 已创建 → `PASSED` 已通过 / `REJECTED` 已驳回 → `ACTIVE_CODE_CREATED` 激活码已创建。
3. 审核通过后生成激活码并写入 `device.t_active_code`（[[tbl_active_code]]），`active_code` 为激活码值，状态 `ENABLE` 未使用。
4. 系统生成激活二维码。
5. 用 POS 扫描该二维码进行激活。
6. 激活成功后：
   - 激活码状态由 `ENABLE` 变为 `USED` 已使用（`device.t_active_code`）。
   - 首次激活的设备硬件信息写入 `device.t_hardware_info`（[[tbl_hardware_info]]），含物理序列号 `SN` 与设备类型 `type`。
   - 设备公钥写入 `device.t_device_key`，`id = t_hardware_info.id`。
   - 商户-门店-设备号关系写入 `device.t_merchant_device`（[[tbl_merchant_device]]），`hardware_id = t_hardware_info.id`。
   - 设备开通的功能配置写入 `device.t_device_ext`，`device_id = t_merchant_device.id`。

## 涉及服务/表
- 服务：basis-merchant（审核）
- 表：
  - `device.t_device_apply_order` 设备申请订单表 [[tbl_device_apply_order]]
  - `device.t_active_code` 设备激活码表 [[tbl_active_code]]
  - `device.t_hardware_info` 设备硬件信息表 [[tbl_hardware_info]]
  - `device.t_device_key` 设备公钥表
  - `device.t_merchant_device` 商户设备关系表 [[tbl_merchant_device]]
  - `device.t_device_ext` 设备功能配置表

## 校验点
- `t_device_apply_order.status` 是否按 `CREATED → PASSED → ACTIVE_CODE_CREATED` 推进；驳回则为 `REJECTED`。
- `t_active_code.active_code` 是否生成，状态在激活前为 `ENABLE`、激活后为 `USED`。
- 激活后 `t_hardware_info` 是否落入设备 `SN`、`type`，且仅在首次激活时保存。
- `t_device_key.id` 必须等于 `t_hardware_info.id`。
- `t_merchant_device.hardware_id` 必须等于 `t_hardware_info.id`，记录商户-门店-设备号关系。
- `t_device_ext.device_id` 必须等于 `t_merchant_device.id`。
