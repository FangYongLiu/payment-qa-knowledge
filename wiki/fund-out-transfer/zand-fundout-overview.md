---
title: ZAND渠道Fundout业务总览
domain: fund-out-transfer
kind: wiki_page
slug: zand-fundout-overview
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:7f334321-3b49-4c87-b6d9-8949925a962a
tags: []
---

# ZAND渠道Fundout业务总览

ZAND Fundout 用于将 PayBy 账户资金通过 ZAND 银行渠道汇出到外部银行账户，覆盖境内 AED、国际 USD/SWIFT、结算、商户后台提现及个人 App 提现等场景。

## 业务定义与场景

- Fundout：从 PayBy 账户出款到外部银行账户，经 ZAND 银行渠道。
- 支持：境内 (AED)、国际 (USD/SWIFT)、Settlement、商户后台 Withdrawal、个人 App 提现。

## ZAND 渠道映射

| 场景 | 渠道 | 币种 | 速度 |
|---|---|---|---|
| 境内 UAE 银行 (IBAN AE开头) API 转账 | ZAND201 | AED | ~12 秒 |
| 国际 SWIFT API 转账 | ZAND203 | USD | 小时级（异步）|
| Settlement 内部转账 | ZAND204 | AED | ~15 秒 |
| Settlement 国际转账 | ZAND207 | USD | 小时级（异步）|
| 商户后台提现（境内）| ZAND210 | AED | ~12 秒 |

## SP / SQ / VS 流程

| 步骤 | 名称 | 说明 |
|---|---|---|
| SP | Submit Payment | 系统向 ZAND 提交付款，银行返回 ChannelRefId |
| SQ | Status Query | 系统周期性轮询 ZAND 状态 |
| VS | Vendor Status (Webhook) | ZAND 异步回调最终状态（COMPLETED/PROCESSED）|

- **境内**：SP -> VS（约 12 秒，无需 SQ）。
- **国际**：SP -> SQ（轮询）-> VS（最终状态）。

## 关键业务规则

- 境内 (ZAND201/210) 通过 SP -> VS 在 ~12s 完成。
- 国际 (ZAND203/207) 异步，需要 SQ 轮询 + VS 回调。
- 商户后台转账需在 *My Authorization* 授权审批后才能处理。
- Settlement 流程需 BMOC 审计审批后执行。
- SQ 轮询在 `RETRY_TIMES = 54` 时停止。

## 参考号格式

| 类型 | 格式 | 示例 |
|---|---|---|
| 境内 ZAND ChannelRefId | `D` 开头 | D773644227520987 |
| 国际 ZAND ChannelRefId | `ZIT` 开头 | ZIT3657863264122 |
| CMF 订单号 | `ZAND` + 渠道前缀 | ZAND20326031611337631 |
| Fundout Order ID | 18 位数字 | 131773657853407506 |

## 产品码 (Product Code)

| Code | 描述 | 渠道 |
|---|---|---|
| 220401 | 境内银行转账 | ZAND201 |
| 220402 | 国际银行转账 (SWIFT) | ZAND203 |
| 230602 | Settlement / 商户提现 | ZAND204、ZAND207、ZAND210 |

## 端到端流程概览

下单 → Fundout Service 创建订单 (mhtfundout) → CMF Router 路由到对应渠道 → SP 提交银行（拿到 ChannelRefId）→（仅国际）SQ 轮询 → VS 回调 → 订单标记 SUCCESS / FAILED。

详细架构与调用链见 [[zand-fundout-system-architecture]]，端到端流程图见 [[flow_zand_fundout]]。

## 相关页面

- 系统架构与 API 调用链：[[zand-fundout-system-architecture]]
- 测试方法指南：[[zand-fundout-test-guide]]
- 常见问题排查：[[zand-fundout-troubleshooting]]
- 核心测试用例集：[[scn_zand_fundout_test_cases]]
- Mock VS 回调工具：[[auto_zand_mock_vs_tool]]
- 出款订单主表：[[tbl_mhtfundout_t_fundout_order]]
- CMF 渠道指令订单表：[[tbl_cmf_tt_inst_order]]
