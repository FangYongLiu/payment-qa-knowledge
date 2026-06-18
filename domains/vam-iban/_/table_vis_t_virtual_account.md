---
id: tbl_vis_t_virtual_account
object_type: Table
domain: vam-iban
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: confluence:tester/219152444
tags:
- table
- vis
- iban
subdomain: null
module: vis
sensitivity: normal
name: vis.t_virtual_account 虚拟账户表
aliases:
- t_virtual_account
related_services: []
related_tables: []
related_scenarios:
- scn_vam_iban_apply_activate
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
存储用户 IBAN 虚拟账户信息。用户在 payby app 充值入口选择 Bank Account Transfer 并点击激活后，申请数据落地到本表，通过 `mid` 与用户关联。后续由 `vis_ibanAccountRetryJob` 批次处理（除 lean 场景外的 fab 用户申请），调用 fab 更新账户状态。

## 关键列
- `mid`：与用户关联的字段（外部通过 mid 关联到本表）。
- `status`：账户状态。
  - `Initial`：申请落库后的初始状态（包括 Vip 用户点击 Free Active 补充姓名后落库时也是 Initial）。
  - `Valid`：经 `vis_ibanAccountRetryJob` 触发并打批发 fab 成功后更新为 Valid。
- iban 信息字段：当 iban 有库存时落库填充 iban 信息；当 iban 没有库存时，前端申请落库时 iban 信息为空，需要人工补充 iban 数据后等待 job 重试。

## 主键/索引
原文未提供。

## 校验点(QA 关注)
- 用户在 app 点击激活后，校验本表是否生成记录、`mid` 是否正确关联、`status=Initial`。
- Vip 用户点击 Free Active 补充姓名信息时无校验，仍需确认数据落库且 status=Initial。
- 非 lean 场景的 fab 用户申请，需确认落库后由 `vis_ibanAccountRetryJob` 批次处理，job 触发后状态由 Initial 更新为 Valid。
- iban 库存为空场景：确认前端申请落库时 iban 字段为空，可人工补充 iban 数据后由 job 重试，最终状态变为 Valid。
- 配合 mock 配置 `vis.notification.mock: Y` 时不会调用 fab，需关注本表状态流转是否符合 mock 预期。
