---
title: 人工资金调拨资金流
domain: manual-fund-settlement
kind: wiki_page
slug: manual-settlement-fund-flow
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:tester/1107722264
tags: []
---

# 人工资金调拨资金流

本页汇总人工资金调拨在 0042、0062 出款，以及 ENBD CMA 账户互转（500110/500111/500113）等场景下的借贷记账资金流。相关业务上下文见 [[manual-fund-settlement-overview]]，结算类型与产品码对应见 [[settlement-type-product-code-mapping]]。

## 0042 出款资金流

| 步骤 | DR | CR |
|---|---|---|
| 1 | 78429990020010001 | 78429990030010002 |
| 2 | 78429990030010002 | 78430030020010002 |

## 0062 出款资金流

| 步骤 | DR | CR |
|---|---|---|
| 1 | 84040030020010001（USD capital reserve-FAB-0062 100 USD） | 84029990030010002（Other Accounts Payable - Pending check for settlement - 0062 USD） |
| 2 | 84029990030010002（Other Accounts Payable - Pending check for settlement - 0062 USD） | 84040010010010001（FundOut Pending for Clearing-FAB-H2H-0062 USD） |

## CMA 账户互转资金流

CMA 账户之间互转需在模板中额外配置 `settlement_code`（如 `CMA3->CMA4`）。

### 500111：CMA2 → CMA3

- DR：78430010210010003（FundIn Pending for Clearing-ENBD CMA3）
- CR：78430030040020001（FundOut Pending for Clearing-CMA2-ENBD204）

### 500113：CMA4 → CMA3

- DR：78430010210010003（FundIn Pending for Clearing-ENBD CMA3）
- CR：78430030040040001（FundOut Pending for Clearing-CMA2-ENBD201）

### 500110：CMA3 → CMA2

- DR：78430010210010002（FundIn Pending for Clearing-ENBD CMA2）
- CR：78430030040030001（FundOut Pending for Clearing-CMA3-ENBD209）

### 500110：CMA3 → CMA4

- DR：78430010210010004（FundIn Pending for Clearing-ENBD CMA4）
- CR：78430030040030001（FundOut Pending for Clearing-CMA3-ENBD210）

## 相关链接

- 端到端流程：[[flow_manual-fund-settlement]]
- 模板与明细落库：[[tbl_t_settlement_template]]、[[tbl_t_settlement_detail]]
