---
id: tbl_device_apply_order
object_type: Table
domain: offline-business
status: active
owner: xiaoqian.wei,wanmei.ding
reviewer: xiaoqian.wei,wanmei.ding
last_reviewed_at: '2026-06-19'
source_type: wiki
source_ref: confluence:AQ/1135345829
tags:
- device
- apply
- activation
subdomain: null
module: null
sensitivity: normal
name: 设备申请订单表
aliases:
- t_device_apply_order
related_services:
- svc_device
---

## 用途
记录通过商户控台提交的设备激活码申请单，承载 basis-merchant 审核流转状态。当设备类型为 Smart POS 时，审核通过后将生成激活二维码并写入 [[tbl_active_code]]，随后用于设备绑定([[tbl_merchant_device]])与硬件登记([[tbl_hardware_info]])。

库表:`device.t_device_apply_order`

## 链路位置
设备开通链路的入口环节(详见 [[flow_device_activation]]):

1. 商户控台提交申请 → 本表插入一条 `status=CREATED` 的申请单。
2. basis-merchant 审核 → `PASSED` 或 `REJECTED`。
3. Smart POS 类型审核通过后系统生成激活码 → 本表 `status=ACTIVE_CODE_CREATED`，同时 [[tbl_active_code]] 落一条 `status=ENABLE` 的激活码记录。
4. 激活码被设备扫码激活后，绑定关系写入 [[tbl_merchant_device]]，设备硬件信息登记到 [[tbl_hardware_info]]。

## 关键列
- `status`:申请单状态
  - `CREATED` 已创建
  - `PASSED` 已通过
  - `REJECTED` 已驳回
  - `ACTIVE_CODE_CREATED` 激活码已创建

## 主键/索引
原文未提供。

## 与关联表关系
- [[tbl_active_code]]:`status=ACTIVE_CODE_CREATED` 时，应存在对应激活码记录(`active_code` 即激活码值，初始 `status=ENABLE`)。
- [[tbl_merchant_device]]:激活码被使用后，产生商户-设备绑定关系。
- [[tbl_hardware_info]]:激活流程完成后登记设备硬件信息(SN 为物理设备序列号，type 为激活的设备类型)。

## 校验点(QA 关注)
- 提交申请后初始状态应为 `CREATED`。
- basis-merchant 审核通过后，状态应先流转为 `PASSED`，激活码生成后变为 `ACTIVE_CODE_CREATED`;驳回则置为 `REJECTED`。
- 状态为 `ACTIVE_CODE_CREATED` 时，[[tbl_active_code]] 必须存在对应记录，`active_code` 非空且 `status=ENABLE`。
- 仅当设备类型为 Smart POS 时走该审核+二维码激活路径;非 Smart POS 不应生成激活码记录。
- 状态流转应单向:`CREATED → PASSED → ACTIVE_CODE_CREATED` 或 `CREATED → REJECTED`，不应回退。
