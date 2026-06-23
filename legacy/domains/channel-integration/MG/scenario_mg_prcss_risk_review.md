---
id: scn_mg_prcss_risk_review
object_type: Scenario
domain: channel-integration
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: wiki:fe1a186f-8431-44b0-a534-d392e3341e7b
tags:
- MG
- PRCSS
- 风控
- 测试场景
subdomain: MG
module: order-status
sensitivity: normal
name: MG PRCSS风控审核场景测试
aliases: []
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 触发/入口
通过 MG 渠道发起印度 bank transfer 汇款，使用特定测试姓名触发渠道风控审核（PRCSS 状态）。

## 前置条件
- 渠道为 MG（间接渠道）
- 收款国家：印度（India）
- 汇款方式：bank transfer
- 收款人信息：
  - First Name: `Buggs`
  - Last Name: `Bunny`

## 操作步骤
1. 在 PayBy 端发起一笔 MG 汇款交易，选择印度 bank transfer 模式
2. 收款人姓名填写 First Name: `Buggs`，Last Name: `Bunny`
3. 完成下单与支付流程，提交至 MG 渠道
4. 等待几分钟后，由 Remittance 定时 Job 调用 Order Status Query 查询订单状态

## DB 校验点
- 订单 PayBy state = `P`，sub state = `CRA (CHANNEL_REMITTANCE_AUDIT)`
- 对应 MG state / sub state = `PRCSS`

## 预期结果
- 过几分钟订单自动变成 `PRCSS` 状态（渠道审核中）
- 该状态要求用户主动提交补充信息，前端有对应流程引导
- App 账单展示：`Transaction on hold`
- Admin portal 展示（修改前）：`Processing - Additional Info Needed`
- Admin portal 展示（修改后）：`AML Pending - Additional Info Needed`
