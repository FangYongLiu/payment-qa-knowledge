---
id: ts_pbs_pricing_strategy_empty
object_type: Troubleshooting
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-24'
source_type: kibana
source_ref: UAT Kibana app_id=pbs / mClass=PaymentPartyFeeCalculatorImpl+DefaultPricingFeeFacade / ERROR，7d 观测 ~12 万次
tags: [payment-core, pbs, 计费, 定价策略]
subdomain: pricing
module: null
sensitivity: normal
name: 获取定价策略失败 — 价格计算策略为空(pbs)
aliases: [价格计算策略为空, CalculateException, 定价策略失败]
related_services: [svc_pbs, svc_tradeii]
related_tables: []
related_scenarios: [scn_online_business_direct_pay, scn_online_business_merchant_split]
related_logs: [service:pbs]
related_failures: []
---

# 获取定价策略失败 — 价格计算策略为空(pbs)

## 症状
Kibana(app_id=pbs,mClass=`PaymentPartyFeeCalculatorImpl` / `DefaultPricingFeeFacade`,ERROR):
`获取定价策略失败 CalculateException: 价格计算策略为空`,抛自 `CalculateHelperImpl.getCalParam`。
**7 天观测约 12 万次。**

## 关联关系
- **涉及服务**:[[svc_pbs]](计费/定价)← 被 [[svc_tradeii]] 调用算费
- **相关日志**:`service:pbs`(PaymentPartyFeeCalculatorImpl / DefaultPricingFeeFacade)
- **关联场景**:[[scn_online_business_direct_pay]]、[[scn_online_business_merchant_split]]

## 可能根因
- 算费时按 (商户/产品/渠道/币种…) 匹配**定价策略为空**——该组合**没有配置定价规则**,或配置未生效/未命中。
- 常见于:新商户/新产品/新渠道未配价、测试用 partner 未配定价、配置 key 不匹配。

## 排查步骤(DB/Kibana)
1. Kibana:app_id=`pbs`,关键字 `价格计算策略为空`,取出算费入参(商户/产品/渠道/币种)。
2. 核对 pbs 定价配置表:该组合是否有有效定价策略(按 partner/product/channel 维度)。
3. 区分:真实漏配 vs 测试 partner 未配价。

## 处理 / 规避
- **QA**:测试前确认所用 partner/product 已配定价;算费失败优先查配置命中。
- 业务侧:补齐定价策略;无策略时给明确业务码,避免高频 ERROR。
> 中高频,部分可能是测试 partner 未配价导致,需结合入参判定。
