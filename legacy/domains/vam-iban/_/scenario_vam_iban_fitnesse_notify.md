---
id: scn_vam_iban_fitnesse_notify
object_type: Scenario
domain: vam-iban
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: confluence:tester/219152444
tags:
- fitnesse
- notify
- test
subdomain: null
module: null
sensitivity: normal
name: VAM IBAN 交易通知 fitnesse 测试
aliases: []
related_services: []
related_tables:
- tbl_vis_t_notify_transaction_flow
- tbl_vis_t_virtual_account
related_scenarios:
- scn_vam_iban_apply_activate
related_logs: []
related_requirements: []
related_failures: []
---

## 触发/入口
通过 fitnesse 页面模拟发送交易通知：
- URL: http://fitnesse.test2pay.com/FrontPage.VisSuitePage.VisNotifyFacade.TestCaseN101

## 前置条件
- 已完成 IBAN 申请与激活流程，vis.t_virtual_account 中存在记录且 status=Valid（经 vis_ibanAccountRetryJob 批次处理打批发 fab 后状态更新为 Valid）
- mock 配置开启（不会真实调用 fab）：
  ```
  vis:
    notification:
        mock: Y
  ```

## 操作步骤
1. 完成 IBAN 申请激活（payby app → 充值 → Bank Account Transfer → 激活）
2. 等待 job vis_ibanAccountRetryJob 批次处理，确认 iban 数据状态=Valid
3. 配置 mock：vis.notification.mock=Y
4. 打开 fitnesse VisNotifyFacade.TestCaseN101 页面，模拟发送交易通知

## DB 校验点
- vis.t_notify_transaction_flow：交易通知流水落库

## 预期结果
- 交易通知通过 fitnesse 成功模拟发送
- vis.t_notify_transaction_flow 表中产生对应交易通知流水记录
