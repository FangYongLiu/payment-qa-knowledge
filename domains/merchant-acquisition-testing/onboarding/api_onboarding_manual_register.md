---
id: api_onboarding_manual_register
object_type: API
domain: merchant-acquisition-testing
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: wiki:7c033704-1056-4e5a-9598-3d67ba9edba4
tags:
- onboarding
- manual-register
- MPGS
subdomain: onboarding
module: manual-register
sensitivity: normal
name: 人工录入登记接口 manualRegister
aliases: []
related_services: []
related_tables:
- tbl_onboarding_t_manual_register_rule
- tbl_onboarding_t_manual_register_rule_field
- tbl_onboarding_t_fund_provider
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
用于人工录入数据方式的报备登记。接收前端/上游提交的手动录入信息(商户、门店、设备),将数据转换为登记 item 与 item_result_map 进行存储,并设置为激活状态,完成将外部供应商处已注册的商户信息回传到 Payby 系统。

适用场景:供应商配置 registerType=Manual,商户已在外部供应商(如 MPGS Onboarding Portal 线下)完成注册,需将结果同步回 Payby。

## 路径/方法
新增接口:manualRegister(归属 onboarding-item-api)。

具体 HTTP path/method 原文未给出。

## 入参
原文未列出完整字段定义,要点:
- 包含人工录入的商户/门店/设备登记信息
- 字段需符合 t_manual_register_rule_field 中针对该 fund_provider_code + ruleType 的字段配置(name、mandatory)
- 录入字段以 key-value 形式提交,用于写入 item_result_map

## 出参
原文未明确出参结构。语义上返回写入结果;若数据写入失败则直接抛错,由上游重试。

## 错误码
原文未列出具体错误码。行为约定:
- 数据写入失败 → 抛错,交由上游重试

## 测试校验点
1. 写入逻辑
   - 接收人工录入数据后,正确转换为 item 与 item_result_map 并落库
   - item 状态置为「激活」
   - 不创建/不依赖 OnboardingOrder(采用方案三:仅写入报备结果信息)
2. 覆盖语义
   - 上报数据字段中 key 之前存在对应数据时,执行覆盖更新
   - 之前不存在的 key,执行新增
3. 与自动报备隔离
   - 调用 manualRegister 不影响自动上报流程,自动上报功能无回归影响
4. 与配置联动
   - 仅当 FundProvider.register_type = MANUAL 时该接口适用
   - 录入字段需匹配 t_manual_register_rule / t_manual_register_rule_field 配置(校验 mandatory 字段是否齐全)
5. 失败处理
   - 数据写入失败时抛错,验证上游可基于异常进行重试
6. 维度覆盖
   - 商户、门店、设备三种维度的登记数据均能正确写入对应 item 记录
