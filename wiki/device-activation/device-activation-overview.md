---
title: 设备激活流程总览（通用）
domain: device-activation
kind: wiki_page
slug: device-activation-overview
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/1135345829
tags: []
---

# 设备激活流程总览（通用）

本页描述 Smart POS 设备从商户申请激活码、basis-merchant 审核、生成激活二维码到 POS 扫码激活的端到端流程，以及涉及的核心数据表。详细流程见 [[flow_device_activation]]。

## 流程步骤

1. 商户在控台申请激活码，设备类型选择 `Smart POS`。
2. 由 basis-merchant 进行审核。
3. 审核通过后系统生成激活二维码。
4. 使用 POS 扫描该二维码完成激活。
5. 设备首次激活时落地设备信息、设备公钥、商户-设备关系及功能扩展配置。

## 相关数据表

- [[tbl_device_apply_order]] `device.t_device_apply_order`：设备申请订单表。
  - 状态枚举：
    - `CREATED` 已创建
    - `PASSED` 已通过
    - `REJECTED` 已驳回
    - `ACTIVE_CODE_CREATED` 激活码已创建
- [[tbl_active_code]] `device.t_active_code`：设备激活码表。
  - 状态枚举：`ENABLE` 未使用、`USED` 已使用
  - `active_code`：激活码值
- [[tbl_hardware_info]] `device.t_hardware_info`：设备信息，设备首次激活后保存。
  - `SN`：物理设备序列号
  - `type`：激活的设备类型
- [[tbl_device_key]] `device.t_device_key`：设备公钥。
  - 关联：`id = t_hardware_info.id`
- [[tbl_merchant_device]] `device.t_merchant_device`：商户-设备关系，设备激活后保存商户-门店-设备号关系。
  - 关联：`hardware_id = t_hardware_info.id`
- [[tbl_device_ext]] `device.t_device_ext`：设备开通的功能配置。
  - 关联：`device_id = t_merchant_device.id`

## 表关联关系

```
t_device_apply_order ──审核通过──▶ t_active_code ──扫码激活──▶ t_hardware_info
                                                                  │
                                                                  ├── t_device_key (id 一致)
                                                                  │
                                                                  └── t_merchant_device (hardware_id)
                                                                            │
                                                                            └── t_device_ext (device_id)
```
