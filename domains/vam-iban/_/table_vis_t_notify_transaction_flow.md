---
id: tbl_vis_t_notify_transaction_flow
object_type: Table
domain: vam-iban
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: confluence:tester/219152444
tags:
- vam-iban
- notify
- fitnesse
subdomain: null
module: null
sensitivity: normal
name: vis.t_notify_transaction_flow 交易通知流水表
aliases: []
related_services: []
related_tables:
- tbl_vis_t_virtual_account
related_scenarios:
- scn_vam_iban_fitnesse_notify
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
存储通过 fitnesse 模拟发出的 VAM IBAN 交易通知数据，作为交易通知接收落库的流水表。

## 关键列
原文未列出具体字段。

## 主键/索引
原文未提供。

## 校验点(QA 关注)
- 通过 fitnesse 入口 `http://fitnesse.test2pay.com/FrontPage.VisSuitePage.VisNotifyFacade.TestCaseN101` 模拟发送交易通知后，校验 `vis.t_notify_transaction_flow` 是否生成对应流水记录。
- 在 mock 配置 `vis.notification.mock: Y` 场景下(不会调用 fab)验证交易通知落库行为。
