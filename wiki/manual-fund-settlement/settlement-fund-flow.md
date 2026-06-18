---
title: 资金调拨账务流水
domain: manual-fund-settlement
kind: wiki_page
slug: settlement-fund-flow
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:55ce713d-d31a-4ab2-83c9-3361843358f6
tags: []
---

# 资金调拨账务流水

本页汇总人工资金调拨场景下，FAB 0042、FAB 0062 出款及 ENBD CMA 账户互转的借贷方科目与资金流明细，对应业务发起后的系统登账行为。完整链路与模板/产品码定义见 [[manual-fund-settlement-overview]]、[[settlement-template-config]]，端到端流程见 [[flow_manual_fund_settlement]]。

## FAB 0042 出款资金流

两段式登账，经由"待清算应付"科目过渡：

- DR：`78429990020010001`
- CR：`78429990030010002`
- DR：`78429990030010002`
- CR：`78430030020010002`

## FAB 0062 出款资金流

USD H2H 出款，先冲减备付金，再过渡到待清算出款科目：

- DR：`84040030020010001` USD capital reserve-FAB-0062 100 USD
- CR：`84029990030010002` Other Accounts Payable - Pending check for settlement - 0062 USD
- DR：`84029990030010002` Other Accounts Payable - Pending check for settlement - 0062 USD
- CR：`84040010010010001` FundOut Pending for Clearing-FAB-H2H-0062 USD

## ENBD CMA 账户互转资金流

CMA 账户之间互转，按 `settlementType` 区分方向，统一登记 FundIn / FundOut Pending for Clearing 科目。

### 500111：CMA2 → CMA3

- DR：FundIn Pending for Clearing-ENBD CMA3（`78430010210010003`）+
- CR：FundOut Pending for Clearing-CMA2-ENBD204（`78430030040020001`）+

### 500113：CMA4 → CMA3

- DR：FundIn Pending for Clearing-ENBD CMA3（`78430010210010003`）+
- CR：FundOut Pending for Clearing-CMA2-ENBD201（`78430030040040001`）+

### 500110：CMA3 → CMA2

- DR：FundIn Pending for Clearing-ENBD CMA2（`78430010210010002`）+
- CR：FundOut Pending for Clearing-CMA3-ENBD209（`78430030040030001`）+

### 500110：CMA3 → CMA4

- DR：FundIn Pending for Clearing-ENBD CMA4（`78430010210010004`）+
- CR：FundOut Pending for Clearing-CMA3-ENBD210（`78430030040030001`）+

## 说明

- CMA 账户互转的方向控制依赖模板上的 `settlement_code`（如 `CMA3->CMA4`）配置，详见 [[settlement-template-config]]。
- 各 `settlementType` 与 `biz_product_code` 的对应关系见 [[manual-fund-settlement-overview]]。
