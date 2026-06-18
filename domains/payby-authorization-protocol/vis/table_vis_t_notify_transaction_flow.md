---
id: tbl_vis_t_notify_transaction_flow
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
- 交易通知
subdomain: vis
module: null
sensitivity: normal
name: 通知交易流水表
aliases: []
related_services: []
related_tables:
- tbl_vis_t_virtual_account
related_scenarios:
- scn_vam_iban_apply_and_transaction
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
记录 VAM IBAN 交易通知流水数据。当通过 fitnesse（VisSuitePage.VisNotifyFacade）模拟发送交易通知时，交易通知数据落地到该表。

## 关键列
原文未提供具体字段定义。

## 主键/索引
原文未提供。

## 校验点(QA 关注)
- 通过 fitnesse 测试入口 `http://fitnesse.test2pay.com/FrontPage.VisSuitePage.VisNotifyFacade.TestCaseN101` 模拟交易通知后，校验 `vis.t_notify_transaction_flow` 是否正确落库。
- 测试交易通知前需确认 mock 配置：`vis.notification.mock: Y`（不会调用 fab）。
- 交易通知关联的虚拟账户应已在 `vis.t_virtual_account` 中存在且状态为 Valid。
