---
id: tbl_vis_t_virtual_account
object_type: Table
domain: deposit-vam
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: confluence:tester/219152444
tags:
- IBAN
- VAM
- iban
- table
- virtual-account
- vis
subdomain: null
module: vis
sensitivity: normal
name: vis.t_virtual_account 虚拟账户表
aliases:
- t_virtual_account
- vis.t_virtual_account
related_services:
- svc_vis
---

## 用途
存储用户 IBAN 虚拟账户信息。用户在 PayBy App 充值入口选择 Bank Account Transfer 并点击激活后,申请数据落地到本表,通过 `mid` 与用户关联。后续由 `vis_ibanAccountRetryJob` 批次处理(除 lean 场景外的 fab 用户申请),调用 fab 更新账户状态。

## 关键列
- `mid`:用户标识,用于关联虚拟账户与用户(外部通过 mid 关联到本表)。
- `status`:账户状态。
  - `Initial`:申请落库后的初始状态(激活后未完成 fab 处理;包括 VIP 用户点击 Free Active 补充姓名后落库时也是 Initial)。
  - `Valid`:经 `vis_ibanAccountRetryJob` 批次触发并调用 fab 成功后更新为 Valid。
- IBAN 信息字段:当 IBAN 有库存时落库填充 IBAN 信息;当 IBAN 没有库存时,前端申请落库时 IBAN 信息为空,需要人工补充 IBAN 数据后等待 job 重试。

## 主键/索引
原文未提供。

## 校验点(QA 关注)
- 普通用户在 App 点击激活后,校验本表是否生成记录、`mid` 是否正确关联、`status=Initial`。
- VIP 用户点击 Free Active 补充姓名信息时无校验,仍需确认数据落库且 `status=Initial`。
- 非 lean 场景的 fab 用户申请,需确认落库后由 `vis_ibanAccountRetryJob` 批次处理,job 触发后状态由 Initial 更新为 Valid。
- IBAN 库存为空场景:确认前端申请落库时 IBAN 字段为空,可人工补充 IBAN 数据后由 job 重试,最终状态变为 Valid。
- 配合 mock 配置 `vis.notification.mock=Y` 时不会调用 fab,需关注本表状态流转是否符合 mock 预期。