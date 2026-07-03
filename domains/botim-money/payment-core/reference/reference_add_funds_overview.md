---
id: reference_add_funds_overview
object_type: Reference
name: Add Funds 充值业务总览
aliases: [add-funds-overview]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
source_type: wiki
source_ref: confluence:PCW/1412988949
tags: [payment-core, wiki-overview]
related_services: []
related_tables: []
---


# Add Funds 充值业务总览

本页介绍 Add Funds（充值）业务的目的、范围与文档修订记录。详细的端到端流程见 [[flow_add_funds_via_bank_card]]。

## 业务目的（Purpose）

- 描述 Add Funds 业务在支付系统中的主流程系统调用，覆盖支付系统核心架构。
- 仅聚焦主流程，已省略部分查询类操作以突出主链路，包括：
  - member 查询
  - merchant 查询
  - 手续费（fee）计算
  - 结算周期（settlement cycle）查询
  - 商户支付方式鉴权（merchant payment method authentication）查询
  - 风控识别（risk control identify）操作
  - 渠道路由（channel routing）
- 设计建议：新系统设计图中不建议引入此类间接依赖系统。

## 业务范围（Scope）

当前 Add Funds 业务文档覆盖：

- **Add funds via Bank Card**：通过银行卡进行充值，详见 [[flow_add_funds_via_bank_card]]。

> 注：BOTIM Transfer 已迁移至 Transfer 业务域；Withdraw via IBAN 不属于本页 scope。

## 修订记录（Revision）

| Date | Content | Revisor |
|---|---|---|
| 20 Oct 2025 | Add funds via Bank Card；BOTIM Transfer；Withdraw via IBAN | Cong Zhou |
| 23 Mar 2026 | 将 BOTIM Transfer 迁移至 Transfer 文档树（ToC - Transfer） | Cong Zhou |
