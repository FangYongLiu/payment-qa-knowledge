---
id: tbl_active_code
object_type: Table
domain: device-pos
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: wiki:de4113f2-55a3-48f8-b592-6714684acf4c
tags:
- 激活码
- 状态
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
- tbl_merchant_device
related_scenarios:
- scn_fiserv_test_tid_creation
- scn_pos_transaction_db_check
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
`device.t_active_code`(设备激活码表)用于存储 Smart POS 设备的激活码值及其使用状态。在设备开通链路中，当设备申请订单(`t_device_apply_order`)审核通过、状态流转为 `ACTIVE_CODE_CREATED` 时，系统会在本表生成对应激活码记录，并据此生成激活二维码，供 Smart POS 终端扫码激活。

## 在交易链路中的位置
本表位于 **设备开通/激活阶段**，是 POS 设备从“申请受理”到“可上送交易”这一过程的关键中间产物：

1. 商户提交设备申请 → `t_device_apply_order` 创建订单记录。
2. 订单审核通过 → `t_device_apply_order` 状态变为 `ACTIVE_CODE_CREATED`，同时在 `t_active_code` 生成一条 `ENABLE` 状态的激活码。
3. 激活码渲染为二维码 → Smart POS 扫码激活 → `t_active_code` 状态变为 `USED`，并触发设备硬件绑定及商户-设备关系建立。
4. 激活完成后，设备方可发起 Fiserv 销售/退款/撤销等收单交易(参见 `tbl_fiserv_sale_order` 等)。

## 关键列
- `active_code`：激活码值，用于生成激活二维码。
- 状态(status)：
  - `ENABLE`：未使用(初始态)
  - `USED`：已使用(激活完成态)

## 主键/索引
原文未提供。

## 关联表关系
- **`t_device_apply_order`(设备申请订单表)**：上游驱动表。订单审核通过(`ACTIVE_CODE_CREATED`)后写入本表，二者状态需一致。
- **`t_hardware_info`(设备硬件信息表)**：扫码激活成功后，激活码所绑定的设备硬件信息会被登记/更新。
- **`t_merchant_device`(商户设备关系表)**：激活完成后，建立商户与设备的绑定关系，作为后续 POS 交易归属依据。

## 校验点(QA 关注)
- **生成校验**：设备申请订单审核通过后，`device.t_active_code` 应生成对应记录，且初始状态为 `ENABLE`。
- **状态一致性**：`t_active_code` 的生成时点应与 `t_device_apply_order.status = ACTIVE_CODE_CREATED` 对齐。
- **激活流转**：Smart POS 扫码激活成功后，对应 `active_code` 状态应由 `ENABLE` 变为 `USED`，且不可重复使用。
- **下游联动**：激活成功后需校验 `t_hardware_info`、`t_merchant_device` 是否同步落库，确保设备可正常发起 Fiserv 收单交易。
- **异常场景**：审核拒绝/订单作废时，不应生成激活码记录；未激活的激活码不应允许 POS 完成激活流程。
