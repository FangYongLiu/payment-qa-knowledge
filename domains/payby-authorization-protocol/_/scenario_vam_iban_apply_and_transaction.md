---
id: scn_vam_iban_apply_and_transaction
object_type: Scenario
domain: authorization-protocol
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: wiki:dc0d6822-f889-4a34-bdfe-72b5e0051862
tags:
- VAM
- IBAN
- fitness
- 测试场景
subdomain: null
module: null
sensitivity: normal
name: VAM IBAN申请与交易测试场景
aliases: []
related_services: []
related_tables:
- tbl_vis_t_virtual_account
- tbl_vis_t_notify_transaction_flow
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 触发/入口
- payby app 充值入口：选择 Bank Account Transfer → 点击激活（Free Active）
- fitness 入口模拟交易通知：http://fitnesse.test2pay.com/FrontPage.VisSuitePage.VisNotifyFacade.TestCaseN101

## 前置条件
- IBAN 库存充足；若库存为空，前端申请落库无 iban 信息，需人工补录 iban 数据后等待 job 重试
- Vip 用户点击 Free Active 后需补充姓名信息（无校验）
- mock 配置（不调用 fab）：
  ```
  vis:
    notification:
      mock: Y
  ```

## 操作步骤
1. 申请 IBAN：在 payby app 充值页选择 Bank Account Transfer，点击激活
   - 激活成功：展示 iban 信息
   - 激活处理中：进入批次处理
2. 批次处理：除 lean 场景外，其他 fab 用户申请都走批次处理，由 job `vis_ibanAccountRetryJob` 触发
   - job 触发后打批发 fab，更新 iban 数据状态
3. 配置 mock，避免实际调用 fab
4. 通过 fitness 用例 TestCaseN101 模拟发送交易通知

## DB 校验点
- `vis.t_virtual_account`（通过 mid 关联）
  - 申请激活后：status = Initial
  - job 处理后：status = Valid
- `vis.t_notify_transaction_flow`：交易通知后落库

## 预期结果
- IBAN 申请成功落库 `vis.t_virtual_account`，初始 status=Initial
- 经 `vis_ibanAccountRetryJob` 批次处理后，iban 状态更新为 Valid
- fitness 模拟交易通知后，交易流水落库 `vis.t_notify_transaction_flow`
