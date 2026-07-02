---
id: tbl_vis_t_notify_transaction_flow
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
- fitnesse
- notify
- vam-iban
- 交易通知
subdomain: null
module: null
sensitivity: normal
name: vis.t_notify_transaction_flow 交易通知流水表
aliases: []
related_services:
- svc_vis
---

## 用途
存储 VAM IBAN 交易通知流水数据,作为交易通知接收落库的流水表。当通过 fitnesse(VisSuitePage.VisNotifyFacade)模拟发送交易通知时,交易通知数据落地到该表。

## 关键列
原文未列出具体字段定义。

## 主键/索引
原文未提供。

## 校验点(QA 关注)
- 通过 fitnesse 测试入口 `http://fitnesse.test2pay.com/FrontPage.VisSuitePage.VisNotifyFacade.TestCaseN101` 模拟发送交易通知后,校验 `vis.t_notify_transaction_flow` 是否生成对应流水记录(正确落库)。
- 测试交易通知前需确认 mock 配置:`vis.notification.mock: Y`(在该配置下不会调用 fab)。
- 交易通知关联的虚拟账户应已在 `vis.t_virtual_account` 中存在且状态为 Valid。
