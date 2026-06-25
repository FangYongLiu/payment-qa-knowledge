---
id: flow_device_activation
object_type: Flow
name: 设备激活端到端流程(Smart POS)
aliases: []
domain: offline-business
status: active
owner: xiaoqian.wei,wanmei.ding
reviewer: xiaoqian.wei,wanmei.ding
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:AQ/1135345829
tags:
- device
- activation
- smart-pos
related_services: [svc_basis_merchant, svc_device]
related_tables:
- tbl_device_apply_order
- tbl_active_code
- tbl_hardware_info
- tbl_merchant_device
related_scenarios: []
---

# 设备激活端到端流程(Smart POS)

## 概述
Smart POS 设备激活的端到端流程:从商户控台发起激活码申请，经 basis-merchant 审核，生成激活二维码，再由 POS 扫码完成激活并落地商户-设备关系与功能配置。链路:「商户控台申请激活码 → basis-merchant 审核 → 生成激活二维码 → POS 扫码激活 → 落库硬件/公钥/绑定/功能配置」。

## 步骤(跨系统)
1. 商户在控台申请激活码，设备类型选择 Smart POS。申请记录写入 [[tbl_device_apply_order]]，状态 `CREATED` 已创建。
2. [[svc_basis_merchant]] 审核:`CREATED → PASSED` 已通过 / `REJECTED` 已驳回。
3. 审核通过后生成激活码并写入 [[tbl_active_code]]，`active_code` 为激活码值，状态 `ENABLE` 未使用;同时申请单状态流转为 `ACTIVE_CODE_CREATED`。
4. 系统生成激活二维码。
5. 用 Smart POS 扫描该二维码进行激活。
6. 激活成功后:
   - 激活码状态由 `ENABLE` 变为 `USED`([[tbl_active_code]])。
   - 首次激活的设备硬件信息写入 [[tbl_hardware_info]]，含物理序列号 `SN` 与设备类型 `type`。
   - 设备公钥写入 `device.t_device_key`，`id = t_hardware_info.id`(对象待补)。
   - 商户-门店-设备号关系写入 [[tbl_merchant_device]]，`hardware_id = t_hardware_info.id`。
   - 设备开通的功能配置写入 `device.t_device_ext`，`device_id = t_merchant_device.id`(对象待补)。
7. 视业务需要，可在商户控台为设备开通附加功能(如 Tips 小费):以「Activate Tips」弹窗形式选择 TIP Model 与上限，确认后参数写入 `device.t_device_ext`。

## 关联关系
- **经过的服务(有序)**:[[svc_basis_merchant]](审核) → [[svc_device]](设备开通落库)(= `related_services`)。
- **关键表**:[[tbl_device_apply_order]] → [[tbl_active_code]] → [[tbl_hardware_info]] → [[tbl_merchant_device]](= `related_tables`);另涉及 `device.t_device_key`、`device.t_device_ext`(对象待补)。
- **关键场景**:待补。

## 校验点
- [[tbl_device_apply_order]] 的 `status` 是否按 `CREATED → PASSED → ACTIVE_CODE_CREATED` 推进;驳回则为 `REJECTED`。
- [[tbl_active_code]] 的 `active_code` 是否生成，状态在激活前为 `ENABLE`、激活后为 `USED`。
- 激活后 [[tbl_hardware_info]] 是否落入设备 `SN`、`type`，且仅在首次激活时保存。
- `t_device_key.id` 必须等于 `t_hardware_info.id`。
- [[tbl_merchant_device]] 的 `hardware_id` 必须等于 `t_hardware_info.id`，记录商户-门店-设备号关系。
- `t_device_ext.device_id` 必须等于 `t_merchant_device.id`。
