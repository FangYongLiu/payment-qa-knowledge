---
id: tbl_device_apply_order
object_type: Table
domain: device-activation
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: wiki:de4113f2-55a3-48f8-b592-6714684acf4c
tags:
- device
- apply
- order
subdomain: null
module: null
sensitivity: normal
name: 设备申请订单表
aliases:
- t_device_apply_order
related_services: []
related_tables:
- tbl_active_code
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
记录通过商户控台提交的设备激活码申请单，承载 basis-merchant 审核流转状态。设备类型为 Smart POS 时，审核通过后将生成激活二维码并写入 [[tbl_active_code]]。

库表：`device.t_device_apply_order`

## 关键列
- `status`：申请单状态
  - `CREATED` 已创建
  - `PASSED` 已通过
  - `REJECTED` 已驳回
  - `ACTIVE_CODE_CREATED` 激活码已创建

## 主键/索引
原文未提供。

## 校验点(QA 关注)
- 提交申请后初始状态应为 `CREATED`。
- basis-merchant 审核通过后，状态应流转为 `PASSED`，并最终在激活码生成后变为 `ACTIVE_CODE_CREATED`；驳回则置为 `REJECTED`。
- 状态为 `ACTIVE_CODE_CREATED` 时，[[tbl_active_code]] 应存在对应记录(`active_code` 即激活码值，初始 `status=ENABLE`)。
- 仅当设备类型为 Smart POS 时走该审核+二维码激活路径。
