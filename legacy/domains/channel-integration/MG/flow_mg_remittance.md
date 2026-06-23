---
id: flow_mg_remittance
object_type: Flow
domain: channel-integration
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: wiki:fe1a186f-8431-44b0-a534-d392e3341e7b
tags:
- MG
- remittance
- flow
subdomain: mg
module: null
sensitivity: normal
name: MG汇款端到端流程
aliases: []
related_services: []
related_tables:
- t_channel_param_mapping
related_scenarios:
- scn_mg_prcss_risk_review
related_logs: []
related_requirements: []
related_failures: []
---

## 概述
MG为间接渠道，无主动推送回调，整体链路依赖主动轮询订单状态。流程从用户点击 Send Money 起，经过路由、汇率查询、字段收集、预校验、下单、状态轮询、入账/退款，构成端到端闭环。

## 步骤(跨系统)
1. **Send Money 路由 → FeeLookup**
   - 用户点击 Send Money，完成路由后若渠道为 MG，调用 FeeLookup 实时查询国家币种下支持的所有模式及汇率（模式下可能有多个 agentid，钱包/bank 场景使用，agentid 配置在 t_channel_param_mapping）。
   - MG 必须实时请求，不使用数据库静态汇率。

2. **进入 Transfer Details → GFFP**
   - 调用 GFFP 获取该收款国家+币种下需要收集的所有字段。
   - 24 小时缓存一次，比对数据库已有字段，缺失字段动态展示输入框。

3. **Confirm 点击 → SendValidation (Pre-Validation)**
   - 对金额、字段、合规性等做预校验，不通过直接阻断并返回错误。

4. **支付完成 → commit 下单**
   - Remittance 在支付完成后调用 commit 提交最终汇款订单，成功后进入结算流程。

5. **Order Status Query 轮询**
   - 由 Remittance 定时 Job 调用，需处理：
     - 成功订单：更新订单、同步账单。
     - 失败订单：触发退款逻辑。
     - 超 60 天未成功的 cash pick up 订单：主动调对方退款接口。
   - 特殊状态处理：
     - PRCSS：渠道审核中，需用户主动提交信息（前端已支持）。
     - AFR：可直接触发主动退款。
     - 成功后仍可能失败：customer 订单详情页提供 refresh 按钮，查询到 refund 则系统侧也做退款。
     - Error=707（PICK_UP_EXPIRE，超 90 天未领取）：挂起为 RS/PUE，继续轮询，已退款则同步退款。

6. **SendReversal 主动退款**
   - 触发场景：basis-customer 订单详情 cancel 按钮；超 60 天未成功的 cash pick up；查询到 AFR 状态。

7. **Funding flow 入账流水**
   - 下单成功推送入款流水；主动退款或查询到失败退款，推送退款流水。

## 涉及服务/表
- **表**：`t_channel_param_mapping`（agentid 等渠道参数配置）
- **外部接口**：FeeLookup、GFFP、SendValidation、commit、Order Status Query、SendReversal
- **内部链路**：路由系统、Remittance、basis-customer、bigdata router（限额决策表）

## 校验点
- FeeLookup：实时返回模式与汇率；`validCurrencyIndicator=false` 时最终确认页需展示 estimated receive amount 与 estimated exchange rate。
- FeeLookup 返回 `<ac:totalReceiveFees>` / `<ac:totalReceiveTaxes>` 时，最终确认页需展示 Receiver's fee。
- GFFP：24 小时缓存命中；缺失字段动态展示。
- SendValidation：失败需阻断交易并返回具体错误。
- commit：超时按完全相同参数重试，依赖幂等逻辑。
- Order Status Query：
  - PRCSS 状态触发用户补充信息流程（验证用例：印度 bank transfer，First Name: Buggs, Last Name: Bunny）。
  - AFR 状态触发主动退款。
  - 成功订单后续可能转 refund，需 refresh 同步。
  - Error=707 挂起为 RS/PUE 并继续轮询。
- 状态映射严格按 [[mg-channel-state-mapping]]，MG 无 sub state（state 与 sub state 相同）。
- 金额限额：通过定时脚本探测获取，配置于 bigdata router 决策表。
