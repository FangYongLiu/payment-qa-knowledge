---
title: 设备激活流程总览（Smart POS）
domain: device-pos
kind: wiki_page
slug: device-activation-overview
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:108bbf00-59ed-4d97-9b82-69660052ab2f
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

## 表间关联

- `t_device_apply_order` 审核通过 → 生成 `t_active_code` 记录
- 扫码激活 → 写入 `t_hardware_info` 与 `t_device_key`（同 `id`）
- 绑定商户/门店 → 写入 `t_merchant_device`（通过 `hardware_id` 关联硬件）
- 功能开通 → 写入 `t_device_ext`（通过 `device_id` 关联商户设备关系）

## TMS 后台管理入口

设备激活相关运营操作集中在 TMS 后台的以下菜单：

- **Device Approval**：设备申请审核
- **Device ActiveCode**：激活码管理
- **Activated Devices**：已激活设备查询
  - 子菜单：`Fiserv Outbound ...`、`Activated Devices`、`Fiserv Exception ...`
- **Devices Channel Ma...**：设备渠道管理
- **POS Settings**：POS 配置
- **Amex Mapping**
- **Operation Logs**：操作日志

### Activated Devices 查询页

用于查询已激活设备列表，支持的过滤条件：

- `Merchant ID`
- `Store ID`
- `Store Name`
- `Device ID`
- 设备类型下拉（如 `SMART_POS`）

列表展示字段：`Merchant ID`、`Merchant Name`、`Store ID`、`Store Name`、`Device ID`、`Device Type`、`Updated Time`、`Action`。

> 注：列表中的 `Device ID` 对应商户-门店-设备关系记录，可经 `hardware_id` 关联到 `t_hardware_info` 中的物理 `SN`。
