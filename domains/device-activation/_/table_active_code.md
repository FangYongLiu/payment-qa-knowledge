---
id: tbl_active_code
object_type: Table
domain: device-activation
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: confluence:AQ/1135345829
tags:
- 激活码
- 设备激活
subdomain: null
module: null
sensitivity: normal
name: 设备激活码表
aliases:
- t_active_code
related_services: []
related_tables:
- tbl_device_apply_order
- tbl_hardware_info
related_scenarios:
- flow_device_activation
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
存储设备激活码值及其使用状态。设备申请订单审核通过后生成激活码（订单状态变为 ACTIVE_CODE_CREATED），用于生成激活二维码供 POS 扫码激活。

表名：`device.t_active_code`

## 关键列
- `active_code`：激活码值
- 状态字段：
  - `ENABLE`：未使用
  - `USED`：已使用

## 主键/索引
原文未提供。

## 校验点(QA 关注)
- 商户控台申请激活码并由 basis-merchant 审核通过后，应在 `t_active_code` 中生成记录，且初始状态为 `ENABLE`。
- 对应 `t_device_apply_order` 状态应同步为 `ACTIVE_CODE_CREATED`。
- POS 扫码激活成功后，`t_active_code.状态` 应由 `ENABLE` 变为 `USED`。
- `active_code` 值应与生成的激活二维码内容一致。
