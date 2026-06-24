---
id: scn_payment_tools_deduct_channel
object_type: Scenario
name: 代扣渠道设置 (Deduct Channel)
aliases: []
domain: payment-tools
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-24'
source_type: repo
source_ref: cgs-apitest/testcases/payment
tags: [payment-tools, cgs-apitest]
related_services: [svc_deduct, svc_member, svc_payment]
related_tables: []
related_logs: []
---

# 代扣渠道设置 (Deduct Channel)

> 业务测试场景。来源 cgs-apitest 回归。

## 场景描述
设置/切换代扣渠道(setDeductChannel),决定自动代扣走哪条渠道。经 deduct 代扣执行。

## 关联关系
- **涉及服务**:[[svc_deduct]]、[[svc_member]]、[[svc_payment]](= `related_services`)
- **覆盖的自动化**:见各 [[auto_*]]
- **读写的表**:待补

## 校验点(QA)
- 渠道设置生效;切换后代扣路由正确。
- 渠道有效性校验;落库。

## 来源与置信
- cgs-apitest 套件整理;服务链由调用线索+callgraph 推断,部分待补。
