---
id: ts_mg_order_state_handling
object_type: Troubleshooting
name: MG 渠道订单状态映射与特殊处理(PRCSS/AFR/REFND/707)
aliases: [MG状态映射, MG特殊规则, MoneyGram state mapping]
domain: payment-tool
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:AQ/1268547712; wiki:fe1a186f-8431-44b0-a534-d392e3341e7b; wiki_image:1ae4c51b-d6d2-4e49-85b5-1a102c47ee69
tags: [mg, moneygram, 状态映射, PRCSS, AFR, REFND, '707']
related_services: []
related_tables: []
related_logs: []
related_failures: []
---

# MG 渠道订单状态映射与特殊处理

## 症状
MG(MoneyGram,间接渠道)订单状态推进异常或停留在审核/退款/过期等中间态;或转账汇总页出现 UI 与金额不一致。MG 不提供主动回调,状态推进主要由 Order Status Query 轮询驱动,退款由 SendReversal 触发。

## 关联关系
- **涉及服务 / 表**:Remittance、MG 渠道(对象待补);`t_channel_param_mapping`(待补)
- **端到端流程**:[[flow_mg_remittance]]
- **相关场景**:[[scn_mg_prcss_risk_review]]

## 状态映射表
**基本规则:MG 自身没有 sub state,映射时 MG state 与 MG sub state 设为相同值。**

| PayBy state | PayBy sub state | MG state/sub state | Memo | App 账单展示 | Admin Portal(修改前) | Admin Portal(修改后) |
|---|---|---|---|---|---|---|
| WP | RRS (REMITTANCE_REQUEST_SUCCESS) | UNCOMMITTED | — | — | — | — |
| PS | CRS (CHANNEL_REMITTANCE_SUBMITED) | AVAIL | — | Processing - Transaction in progress | Submitted | Processing |
| P | CRA (CHANNEL_REMITTANCE_AUDIT) | PRCSS | MG 新增,被风控 | Transaction on hold | Processing - Additional Info Needed | AML Pending - Additional Info Needed |
| S | CRC (CHANNEL_REMITTANCE_COMPLETED) | RECVD | — | Completed | Completed | Completed |
| P | CRR (CHANNEL_REMITTANCE_REJECT) | AFR | 被风控审核拒绝,只能撤销或退款 | Transaction on hold | Processing - Available for refund | AML Pending - Available for refund |
| F | CCR (CHANNEL_CANCEL_REMITTANCE) | CANCL | — | Transaction Cancelled | Transaction Cancelled | Transaction Cancelled |
| F | CR (CHANNEL_REFUNDED) | REFND | MG 新增,已退款 | Transaction Failed | Transaction Failed | Transaction Failed |
| F | OC (ORDER_CLOSE) | - | PayBy 关闭未支付订单 / 汇款被风控失败 | — | — | — |
| F | SF (SUBMIT_FAIL) | - | 提交渠道失败 | — | — | — |
| CP | * | - | 用户/运营/系统发起撤销 | — | — | — |
| C | CCR → CR | - | 用户/运营主动撤销 | Transaction Failed | — | — |
| RS | PUE (PICK_UP_EXPIRE) | - | 超 90 天未领取 | Transaction Failed | — | — |

## 可能根因 / 关键状态说明
- **PRCSS(渠道审核中)**:MG 风控触发,要求用户主动补充信息,前端已实现流程。复现:印度 bank transfer,First Name `Buggs`,Last Name `Bunny`,下单几分钟后自动变 PRCSS(详见 [[scn_mg_prcss_risk_review]])。
- **AFR(可退款)**:被风控审核拒绝,查询到即可调 SendReversal 主动退款。
- **REFND(已退款)**:MG 订单成功(RECVD)后仍可能失败转退款,因此 basis-customer 订单详情页对成功订单提供 **Refresh 按钮**,点击重查;若变 refund 则系统同步退款。
- **RS/PUE(PICK_UP_EXPIRE)**:90 天未领取,MG 内部置过期,查询返回 `Error=707, Message=Please call MoneyGram customer service center to complete this transaction (code 45)`;PayBy 挂起为 RS/PUE 继续轮询,已退款则同步退款(对应对账单待确认)。
- **超 60 天未成功的 cash pick up**:查询仍处理中时主动调 SendReversal。

## 排查步骤
- DB:查订单 state/sub state 与 MG state 对照(上表);MG 无 sub state。
- Kibana:看 Remittance Order Status Query 轮询日志、各特殊状态(PRCSS/AFR/707)的处理分支。
- 入账与回调:MG 无主动回调,完全依赖主动轮询;下单成功推入款流水,主动退款/查到失败退款推退款流水。

## 处理 / 规避
- 状态查询与推进契约见 Order Status Query;主动退款触发条件见 SendReversal(见 [[flow_mg_remittance]] 接口要点)。
- App 账单与 Admin Portal 文案有「修改前/修改后」两套版本,以表格列为准。

## 已知 UI / 数据问题(转账汇总页)
基于 AED→JPY 转账示例截图识别:
1. **币种代码拼写错误**:Estimated Receive Amount 行显示 `JYP`,应为 `JPY`(同页 Estimated Exchange Rate 的 JPY 正确,前后不一致)。
2. **金额合计不一致**:明细 `1,000 + 1 + 2 = 1,003`,但 Amount Payable 显示 `1,015.75`,差额约 12.75,疑有未展示的费用/税项或取整缺陷。
3. **Estimated Receive Amount 计算来源不明**:以展示汇率 39.2812 验证,用 Transfer Amount 或 Amount Payable 推算均无法精确匹配显示值 39,379.41,计算口径需确认。
> 上述属待修复/待确认项,标「待补」。
