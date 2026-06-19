---
title: 设备激活流程总览（Smart POS）
domain: device-pos
kind: wiki_page
slug: device-activation-overview
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:9918fe6e-cabe-4d03-a36f-f32603dea3fe
tags: []
---

# 设备激活流程总览（Smart POS）

Smart POS 设备激活遵循「商户控台申请激活码 → basis-merchant 审核 → 生成激活二维码 → POS 扫码激活」的端到端链路，激活完成后落库设备硬件信息、公钥、商户-门店-设备关系及功能配置。

## 流程步骤

1. 商户登录 PayBy 商户控台，进入 `Apply For New Device`（新设备申请）流程，设备类型选择 `Smart POS`。
2. 在 `Store Information`（门店信息）步骤的 `Add or select a store` 下拉中：
   - 选择已有门店（如 `ADCB Store`、`Cars Taxi L.L.C Abu Dhabi office` 等），或
   - 选择 `Add A New Store` 新建门店，并填写：
     - `Store Name`
     - `Address Line1`（街道地址、邮箱、单元、楼宇、楼层等）
     - `Address Line3`（城市、国家）
     - `Location on Map`（在嵌入的 Google Map 上选点）
3. 提交激活码申请，由 `basis-merchant` 服务审核。
4. 审核通过后系统生成激活二维码。
5. 使用 Smart POS 扫描二维码完成激活。
6. 首次激活后写入设备信息及商户-门店-设备绑定关系。

> 提示：替换出租车 POS（taxi POS）场景同样走此「申请新设备」流程，并在门店信息步骤选择对应已有门店。

详见 [[flow_device_activation]]。

## 商户控台导航参考

商户控台左侧菜单包含：Home、Transaction、Balance、Secondary Merchants、Terminals、Data Report、Staff Management、Authorization、Operation History、`Device Management`、Tax Invoice、Change Password。设备申请入口位于 `Device Management`。

## 关键数据表

- [[tbl_device_apply_order]]（`device.t_device_apply_order`）：设备申请订单
  - 状态枚举：
    - `CREATED` 已创建
    - `PASSED` 已通过
    - `REJECTED` 已驳回
    - `ACTIVE_CODE_CREATED` 激活码已创建
- [[tbl_active_code]]（`device.t_active_code`）：设备激活码
  - 状态枚举：`ENABLE` 未使用、`USED` 已使用
  - `active_code`：激活码值
- [[tbl_hardware_info]]（`device.t_hardware_info`）：设备硬件信息
  - 设备首次激活后写入
  - `SN`：物理设备序列号
  - `type`：激活的设备类型
- `device.t_device_key`：设备公钥，`id = t_hardware_info.id`
- [[tbl_merchant_device]]（`device.t_merchant_device`）：商户-门店-设备关系
  - 设备激活后写入
  - `hardware_id = t_hardware_info.id`
- `device.t_device_ext`：设备开通的功能配置
  - `device_id = t_merchant_device.id`

## 表间关联

- `t_device_apply_order` 审核通过 → 生成 `t_active_code` 记录
- 扫码激活 → 写入 `t_hardware_info` 与 `t_device_key`（同 `id`）
- 绑定商户/门店 → 写入 `t_merchant_device`（通过 `hardware_id` 关联硬件）
- 功能开通 → 写入 `t_device_ext`（通过 `device_id` 关联商户设备关系）
