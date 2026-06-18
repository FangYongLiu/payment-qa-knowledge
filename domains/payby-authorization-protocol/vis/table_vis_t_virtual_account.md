---
id: tbl_vis_t_virtual_account
object_type: Table
domain: payby-authorization-protocol
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: wiki:dc0d6822-f889-4a34-bdfe-72b5e0051862
tags:
- VAM
- IBAN
- virtual-account
subdomain: vis
module: null
sensitivity: normal
name: 虚拟账户表
aliases:
- vis.t_virtual_account
related_services: []
related_tables:
- tbl_vis_t_notify_transaction_flow
related_scenarios:
- scn_vam_iban_apply_and_transaction
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
存储用户在 PayBy App 通过 Bank Account Transfer 入口申请的 IBAN 虚拟账户信息。用户激活 IBAN 后落库到该表，并通过 `mid` 与用户关联。

## 关键列
- `mid`：用户标识，用于关联虚拟账户与用户。
- `status`：账户状态。
  - `Initial`：申请落库初始状态（激活后未完成 fab 处理）。
  - `Valid`：经 `vis_ibanAccountRetryJob` 批次处理并调用 fab 更新后的有效状态。
- IBAN 信息字段：当 IBAN 库存为空时，前端申请落库时该信息为空，需人工补充 IBAN 数据后等待 job 重试。

## 主键/索引
原文未提供。

## 校验点(QA 关注)
- 普通用户激活后，记录应落入 `vis.t_virtual_account`，初始 `status=Initial`。
- VIP 用户点击 Free Active 后补充姓名信息（无校验），同样落库本表。
- 除 lean 场景外，fab 用户申请均走批次处理，由 `vis_ibanAccountRetryJob` 触发后更新 `status=Valid`。
- 当 IBAN 无库存时，落库记录中无 IBAN 信息；需人工补充 IBAN 数据，等待 job 重试后状态更新。
- mock 配置 `vis.notification.mock=Y` 时不会调用 fab，需关注此场景下状态流转是否符合预期。
