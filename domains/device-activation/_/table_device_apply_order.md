---
id: tbl_device_apply_order
object_type: Table
domain: device-activation
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: confluence:AQ/1135345829
tags:
- 设备激活
- 申请单
subdomain: null
module: null
sensitivity: normal
name: 设备申请订单表
aliases:
- t_device_apply_order
- device.t_device_apply_order
related_services: []
related_tables:
- tbl_active_code
related_scenarios:
- flow_device_activation
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
记录通过商户控台提交的设备激活码申请单。设备类型为 Smart POS 时，由 basis-merchant 进行审核；审核通过后生成激活二维码并创建激活码（写入 `device.t_active_code`）。

## 关键列
- `status`：申请单状态
  - `CREATED`：已创建
  - `PASSED`：已通过
  - `REJECTED`：已驳回
  - `ACTIVE_CODE_CREATED`：激活码已创建

## 主键/索引
原文未提供。

## 校验点(QA 关注)
- 商户控台提交设备类型 Smart POS 的申请后，应在 `device.t_device_apply_order` 中查询到对应记录，初始 `status=CREATED`。
- basis-merchant 审核通过后，状态应流转为 `PASSED`，并最终变为 `ACTIVE_CODE_CREATED`，同时在 `device.t_active_code` 生成对应激活码（`active_code` 有值，状态 `ENABLE`）。
- 审核驳回场景，状态应为 `REJECTED`，且不应在 `t_active_code` 中生成激活码。
- 状态取值仅限 `CREATED / PASSED / REJECTED / ACTIVE_CODE_CREATED`，不应出现其他值。
