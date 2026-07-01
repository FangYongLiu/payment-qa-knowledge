---
id: api_onboarding_manual_register
object_type: API
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: confluence:PMDPayment/684425357
tags:
- onboarding
- manual-register
subdomain: onboarding
module: item
sensitivity: normal
name: 人工录入报备接口 manualRegister
aliases: []
related_services:
- svc_onboarding
---

## 用途
新增 manualRegister 接口，用于接收人工录入的报备数据。接口内部将录入的数据转换为登记 item、item_result_map 数据进行存储，并设置为激活状态。适用于商户已在外部供应商(如 MPGS Onboarding Portal 线下)完成注册后，将登记信息同步回 Payby 系统的场景。

## 路径/方法
原文未给出具体 HTTP 路径与方法，仅说明为 onboarding 服务下新增接口 manualRegister(详见 onboarding-item-api 接口图)。

## 入参
原文未列出具体字段定义。语义上接收人工录入的商户/门店/设备登记数据，字段以 key-value 形式存在(对应 item_result_map 中的 key)。

## 出参
原文未明确出参结构。

## 错误码
原文未列出错误码。说明：如数据写入失败则直接抛错由上游重试。

## 测试校验点
- 调用接口后，录入数据应被转换并写入 item 与 item_result_map 表
- item 状态应为"激活"
- 若上报数据字段中的 key 已存在对应数据，应进行覆盖写入
- 数据写入失败时应抛错，便于上游重试
- 不应创建/维护 OnboardingOrder(方案三：不走订单流转)
- 与自动报备流程相互隔离，不影响自动上报功能
- 对于 registerType=Manual 的供应商，需配合 [[api_onboarding_get_config]] 返回的人工登记规则(来自 [[tbl_onboarding_t_manual_register_rule]] / [[tbl_onboarding_t_manual_register_rule_field]])校验录入字段(如 mandatory)
