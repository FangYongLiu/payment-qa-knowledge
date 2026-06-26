---
title: ZAND渠道Fundout业务总览
domain: fund-out-transfer
kind: wiki_page
slug: zand-fundout-overview
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/2049867832
tags: []
related_services:
  - svc_cmf
  - svc_fundout
  - svc_merchant_fundout
  - svc_qpay_zand
related_tables:
  - tbl_cmf_tt_inst_order
  - tbl_cmf_tt_inst_order_result
  - tbl_mhtfundout_t_fundout_order
---

# ZAND渠道Fundout业务总览

ZAND Fundout 指通过 ZAND 银行渠道将资金从 PayBy 账户转出至外部银行账户，覆盖境内（AED）与跨境（USD/SWIFT）转账、清结算、商户后台提现以及个人 App 提现。

## 业务定义与场景

- **Fundout**：把钱从 PayBy 账户转出到外部银行账户。
- 支持的业务入口：
  - API 直连（合作商户）
  - Merchant Portal（商户后台）转账与提现
  - BMOC 发起的清结算
  - Botim App 个人提现

## ZAND 渠道映射

| 场景 | 渠道 | 币种 | 速度 |
|---|---|---|---|
| 境内 UAE 银行转账（IBAN 以 AE 开头）via API | ZAND201 | AED | ~12 秒 |
| 跨境 SWIFT 转账 via API | ZAND203 | USD | 小时级（异步） |
| 清结算境内转账 | ZAND204 | AED | ~15 秒 |
| 清结算跨境转账 | ZAND207 | USD | 小时级（异步） |
| 商户后台提现（境内） | ZAND210 | AED | ~12 秒 |

## 产品码（Product Code）

| Code | 说明 | 渠道 |
|---|---|---|
| 220401 | 境内转账到银行 | ZAND201 |
| 220402 | 跨境转账到银行（SWIFT） | ZAND203 |
| 230602 | 清结算 / 商户提现 | ZAND204、ZAND207、ZAND210 |

## SP / SQ / VS 流程

| 步骤 | 名称 | 说明 |
|---|---|---|
| SP | Submit Payment | 系统向 ZAND 提交付款，银行返回 ChannelRefId |
| SQ | Status Query | 系统周期性轮询 ZAND 查询状态 |
| VS | Vendor Status (Webhook) | ZAND 回调最终状态（COMPLETED / PROCESSED） |

- **境内**：SP -> VS（无需 SQ，~12 秒完成）
- **跨境**：SP -> SQ（轮询）-> VS（最终状态）

端到端流程详见 [[flow_zand_fundout]]。

## 端到端流程概览

1. 用户/商户发起转账。
2. Fundout 服务在 `mhtfundout` 库创建订单（参见 [[tbl_mhtfundout_t_fundout_order]]、[[tbl_mhtfundout_t_fundout_bankcard_order]]）。
3. CMF Router 选择匹配的 ZAND 渠道，落 [[tbl_cmf_tt_inst_order]]。
4. SP 提交至 ZAND，获取 ChannelRefId。
5. 仅跨境：SQ 周期性轮询。
6. VS Webhook 回调最终状态，结果写入 [[tbl_cmf_tt_inst_order_result]]。
7. 订单标记为 SUCCESS 或 FAILED。

## 关键业务规则

- 境内（ZAND201/210）通过 SP -> VS 在 ~12 秒内完成。
- 跨境（ZAND203/207）异步处理，需 SQ 轮询 + VS 回调。
- Merchant Portal 转账需在「My Authorization」中完成授权后才会处理。
- 清结算流程必须经 BMOC 审核（Audit）通过后才执行。
- SQ 轮询行为：
  - 前 ~2 分钟轮询频繁
  - 间隔逐步加大
  - `RETRY_TIMES > 35` 后达到小时级
  - `RETRY_TIMES = 54` 时停止轮询

## 单据号与引用号格式

| 类型 | 格式 | 示例 |
|---|---|---|
| 境内 ZAND reference | 以 `D` 开头 | `D773644227520987` |
| 跨境 ZAND reference | 以 `ZIT` 开头 | `ZIT3657863264122` |
| CMF 订单号 | `ZAND` + 渠道号开头 | `ZAND20326031611337631` |
| Fundout 订单 ID | 18 位数字 | `131773657853407506` |

## 订单状态值

| 库表 | 字段 | 取值 |
|---|---|---|
| `mhtfundout.t_fundout_order` | `status` | CREATED, PLACED, SUCCESS, FAILURE |
| `cmf.tt_inst_order` | `STATUS` | I（处理中）、S（成功）、F（失败）、U（未知） |
| `cmf.tt_inst_order_result` | `API_TYPE` | SP, SQ, VS |

## 相关页面

- 系统架构与调用链：[[zand-fundout-system-architecture]]
- 测试方法与环境：[[zand-fundout-testing-guide]]
- 核心用例集：[[scn_zand_fundout_test_cases]]
- 常见问题排查：[[zand-fundout-troubleshooting]]
- Mock VS 回调工具：[[auto_zand_mock_vs_tool]]
