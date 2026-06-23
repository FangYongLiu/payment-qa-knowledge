---
title: 设备激活流程总览（Smart POS）
domain: device-pos
kind: wiki_page
slug: device-activation-overview
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:d2621f22-6224-43d6-9c09-25beff7ec83b
tags: []
---

# 设备激活流程总览（Smart POS）

Smart POS 设备激活遵循「商户控台申请激活码 → basis-merchant 审核 → 生成激活二维码 → POS 扫码激活」的端到端链路，激活完成后落库设备硬件信息、公钥、商户-门店-设备关系及功能配置。

## 流程步骤

1. 商户在商户控台提交设备激活码申请，设备类型选择 `Smart POS`。
2. 由 `basis-merchant` 服务进行审核。
3. 审核通过后系统生成激活二维码。
4. 使用 Smart POS 扫描二维码完成激活。
5. 首次激活后写入设备信息及商户-门店-设备绑定关系。
6. 视业务需要，在商户控台对设备开通附加功能（如 Tips 小费），开通参数写入功能配置表。

详见 [[flow_device_activation]]。

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
  - 用于承载激活后开通的功能参数（如 Tips 小费的模型与上限）

## 表间关联

- `t_device_apply_order` 审核通过 → 生成 `t_active_code` 记录
- 扫码激活 → 写入 `t_hardware_info` 与 `t_device_key`（同 `id`）
- 绑定商户/门店 → 写入 `t_merchant_device`（通过 `hardware_id` 关联硬件）
- 功能开通 → 写入 `t_device_ext`（通过 `device_id` 关联商户设备关系）

## 激活后功能开通

设备激活完成后，可在商户控台为设备开通附加功能，开通入口通常以「Activate Tips」类弹窗形式呈现。

### Tips（小费）开通示例

弹窗标题：`Activate Tips`。

字段：

- `TIP Model`（必填）：当前示例值为 `Tier1 - Tip after purchases`
  - 说明：Support entering tip amount together with purchase amount.（支持在交易金额之外一并录入小费金额）
- `Set maximum tip amount`（必填）：小费上限
  - 数值输入框（示例预填值 `99.00`）
  - 单位下拉框：`Amount`（金额）等可选单位（如百分比）
  - 说明：Set the fixed maximum tip amount.（设置固定的小费上限）

操作：

- `Confirm`：确认开通，参数随之写入 `t_device_ext`
- `×`：关闭弹窗，取消本次开通

Loading...

Loading...
</content>
</page>
