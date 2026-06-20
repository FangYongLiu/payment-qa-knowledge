---
id: tbl_mhtfundout_t_fundout_bankcard_order
object_type: Table
domain: fund-out-transfer
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: wiki:7f334321-3b49-4c87-b6d9-8949925a962a
tags:
- mhtfundout
- bankcard
- fundout
subdomain: null
module: null
sensitivity: normal
name: 出款银行卡订单表 t_fundout_bankcard_order
aliases: []
related_services: []
related_tables:
- tbl_mhtfundout_t_fundout_order
- tbl_cmf_tt_inst_order
related_scenarios:
- scn_zand_fundout_test_cases
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
位于 `mhtfundout` 库，存储出款订单中的银行卡（收款账户）相关明细，包括出款币种、金额、网络代码与汇率等。与主订单表 `t_fundout_order` 配合使用，由 Fundout Service 在订单创建阶段写入，供后续 CMF Router 路由到对应银行渠道（ZAND201 / ZAND203 / ZAND204 / ZAND207 / ZAND210）。

## 关键列
| 列名 | 说明 |
|---|---|
| fundout_crcy_code | 出款币种代码（如 AED / USD） |
| fundout_amount | 出款金额 |
| network_code | 网络/通道代码（区分本地 vs SWIFT 等） |
| rate | 汇率 |

## 主键/索引
原文未提供。

## 校验点(QA 关注)
- 币种与渠道一致性：
  - AED → ZAND201 / ZAND204 / ZAND210（domestic）
  - USD → ZAND203 / ZAND207（international SWIFT）
- `fundout_amount` 应与 `cmf.tt_inst_order.AMOUNT`、VS 回调中金额保持一致。
- `network_code` 须与产品码（220401 本地 / 220402 国际 SWIFT / 230602 结算或商户提现）以及实际路由渠道相符；若出现路由到 TEST201 而非 ZAND203，需检查 partner 路由配置。
- 国际 SWIFT 场景下，确认 `rate` 字段填充正确，与费用（如 157.50 AED）核对。
- 与 `t_fundout_order` 通过 `global_id` / partner 信息关联；订单状态推进（CREATED → PLACED → SUCCESS/FAILURE）期间该明细行不应缺失。
