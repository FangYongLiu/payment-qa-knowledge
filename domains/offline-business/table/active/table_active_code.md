---
id: tbl_active_code
object_type: Table
name: 设备激活码表(device.t_active_code)
aliases:
- t_active_code
- device.t_active_code
domain: offline-business
status: active
owner: xiaoqian.wei,wanmei.ding
reviewer: xiaoqian.wei,wanmei.ding
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:AQ/1135345829
tags:
- 激活码
- Smart POS
- 设备开通
related_services: [svc_device]
related_scenarios: []
---

# 设备激活码表(device.t_active_code)

## 用途
`device.t_active_code` 存储 Smart POS 设备的激活码值及其使用状态。在设备开通链路中，当设备申请订单([[tbl_device_apply_order]])审核通过、状态流转为 `ACTIVE_CODE_CREATED` 时，系统在本表生成对应激活码记录，并据此生成激活二维码，供 Smart POS 终端扫码激活。激活完成后，设备方可发起后续收单交易。详见 [[flow_device_activation]]。

库表:`device.t_active_code`

## 关联关系
- **所属服务**:[[svc_device]](= frontmatter `related_services`,tbl→service 边)
- **谁读写它**:device 服务在激活链路中写入/更新(由 [[svc_device]] 声明)。
- **上游驱动表**:[[tbl_device_apply_order]](审核通过流转到 `ACTIVE_CODE_CREATED` 后生成激活码)。
- **下游联动表**:[[tbl_hardware_info]](扫码激活成功后登记设备硬件信息)、[[tbl_merchant_device]](激活完成后建立商户-门店-设备绑定)。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `active_code` | 待补 | 激活码值，用于生成激活二维码，供 Smart POS 扫码使用 |
| `status` | 待补 | 状态:`ENABLE` 未使用(初始态)/ `USED` 已使用(激活完成态) |

## 主键 / 索引
- 待补:原文未提供。

## 校验点(QA 关注)
- **生成校验**:设备申请订单审核通过后，本表应生成对应记录，初始状态为 `ENABLE`。
- **状态一致性**:激活码生成时点应与 [[tbl_device_apply_order]] 的 `status = ACTIVE_CODE_CREATED` 对齐。
- **激活流转**:Smart POS 扫码激活成功后，对应 `active_code` 状态应由 `ENABLE` 变为 `USED`，且不可重复使用。
- **下游联动**:激活成功后需校验 [[tbl_hardware_info]]、[[tbl_merchant_device]] 是否同步落库，确保设备可正常发起后续收单交易。
- **异常场景**:审核驳回(`REJECTED`)或订单仍为 `CREATED`/`PASSED` 未到 `ACTIVE_CODE_CREATED` 时，不应生成激活码记录;未激活(`ENABLE`)的激活码不应允许重复扫码完成激活。
