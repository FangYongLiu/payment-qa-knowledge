---
id: flow_mg_remittance
object_type: Flow
name: MG (MoneyGram) 汇款端到端流程
aliases: [MG汇款流程, MoneyGram remittance]
domain: payment-tool
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:AQ/1268547712; wiki:fe1a186f-8431-44b0-a534-d392e3341e7b
tags: [mg, moneygram, remittance, 汇款, 间接渠道]
related_services: []
related_tables: []
related_scenarios: [scn_mg_prcss_risk_review]
---

# MG (MoneyGram) 汇款端到端流程

## 概述
MG 是 PayBy 接入的**间接汇款渠道**(无主动推送回调,整体链路依赖主动轮询订单状态),覆盖大多数收款国家与币种。因不同国家所需字段差异较大,接入时增加了**动态字段收集**与**实时汇率查询**逻辑。流程从用户点击 Send Money 起,经路由、汇率查询、字段收集、预校验、下单、状态轮询、入账/退款,构成端到端闭环。
注:服务对象 svc_qpay_mg 待补(域内尚未建 MG 服务对象)。

## 步骤(跨系统)
1. **Send Money 路由 → FeeLookup(汇率查询)**
   - 完成路由后渠道为 MG 时,调用 FeeLookup 实时查询国家币种下支持的所有模式及汇率。**MG 必须实时请求,不使用数据库静态汇率。**
   - 同一模式下可能有多个 agentid(钱包/bank 场景),agentid 配置在 `t_channel_param_mapping`。
   - 关键返回:`validCurrencyIndicator=false` → 最终确认页展示 estimated receive amount 与 estimated exchange rate;`<ac:totalReceiveFees>`/`<ac:totalReceiveTaxes>` → 展示 Receiver's fee。
2. **进入 Transfer Details → GFFP(动态字段查询)**
   - 获取该收款国家+币种下需收集的所有字段;**24 小时缓存一次**,比对数据库已有字段,缺失字段动态展示输入框。不同国家返回字段差异较大。
3. **Confirm → SendValidation(下单前预校验)**
   - 对金额、字段、合规性做预校验;不通过直接阻断并返回具体错误,不进入 commit。
4. **支付完成 → commit(下单)**
   - 支付完成后由 Remittance 调用 commit 提交最终汇款订单,成功后进入结算流程并推送入款流水。订单进入 CRS(CHANNEL_REMITTANCE_SUBMITED)→ MG state=AVAIL。
5. **Order Status Query(轮询)**
   - 由 Remittance 定时 Job 调用:成功订单更新+同步账单;失败订单触发退款;超 60 天未成功的 cash pick up 订单主动调对方退款接口。
   - 特殊状态:PRCSS(渠道审核中,需用户补充信息)、AFR(可直接主动退款)、成功后再失败(详情页 refresh 按钮重查,变 refund 则系统退款)、Error=707(PICK_UP_EXPIRE 超 90 天未领取,挂起 RS/PUE 继续轮询)。
6. **SendReversal(主动退款)**
   - 触发:basis-customer 订单详情 cancel 按钮;超 60 天未成功的 cash pick up;查询到 AFR。
7. **Funding flow(入账流水)**
   - 下单成功推送入款流水;主动退款或查询到失败退款推送退款流水。

## 关联关系
- **经过的服务(有序)**:Remittance → MG 渠道(外部);内部链路含路由系统、basis-customer、bigdata router(限额决策表)。服务对象待补。
- **关键表**:`t_channel_param_mapping`(agentid 等渠道参数配置,对象待补)。
- **关键场景**:[[scn_mg_prcss_risk_review]](= `related_scenarios`)
- **状态映射 / 特殊规则**:见 [[ts_mg_order_state_handling]]。

## 接口要点(MG 外部接口)
| 接口 | 用途 | 关键校验 |
|---|---|---|
| FeeLookup | 实时查模式与汇率 | 实时数据非静态;多 agentid 取数(读 t_channel_param_mapping);差异化展示字段 |
| GFFP | 查动态收集字段 | 进 Transfer Details 调用;24h 缓存;缺失字段动态展示;多国家组合验证 |
| SendValidation | 下单前预校验 | Confirm 时触发一次;不通过阻断不进 commit;字段与 GFFP 一致 |
| commit | 提交汇款订单 | 支付完成后调用;**超时按完全相同参数重发(幂等)**,不产生重复订单 |
| Order Status Query | 轮询订单状态 | 定时 Job 驱动;处理 PRCSS/AFR/707 等特殊状态 |
| SendReversal | 主动退款 | cancel / 超 60 天未成功 cash pickup / AFR 触发 |

## 校验点
- FeeLookup 返回实时汇率;`validCurrencyIndicator=false` 与 totalReceiveFees/Taxes 的差异化展示。
- GFFP 24h 缓存命中;缺失字段动态展示;缓存过期(>24h)重新调用。
- SendValidation 失败阻断交易并返回具体错误。
- commit 超时按完全相同参数重试,依赖幂等逻辑。
- 状态映射严格按 [[ts_mg_order_state_handling]],**MG 无 sub state(state 与 sub state 相同)**。
- 金额限额:MG 不直接提供,通过定时脚本递增金额探测获取,配置于 bigdata router 决策表。
