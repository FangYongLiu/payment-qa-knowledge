---
id: scn_payment_core_manual_fund_settlement
object_type: Scenario
name: 人工资金调拨-产品码映射与资金流校验
aliases:
- settlement-fund-flow
- settlement-type-product-code-mapping
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:AQ/1138425935; wiki:11dc5fef-89b3-45ad-81a8-95bfefa0519a
tags:
- settlement
- fund-flow
- accounting
related_services:
- svc_counter
- svc_reconciliation
related_tables:
- tbl_reconciliation_t_settlement_template
- tbl_reconciliation_t_settlement_detail
related_logs: []
---

# 人工资金调拨-产品码映射与资金流校验

校验人工资金调拨在不同 `settlementType` / `biz_product_code` 下,系统调拨产生的借贷(DR/CR)分录是否正确。端到端流程见 [[flow_manual_fund_settlement]]。

## 触发/入口
- 入口:counter — settlement detail — apply settlement(选模板 → 输入金额 → 提交审核 → 审核通过 → 系统调拨)
- 触发登账的前提:结算申请 Audit Status=PASS。

## 关联关系
- **涉及服务**:[[svc_counter]](操作入口)、[[svc_reconciliation]](模板/配置/登账)(= `related_services`)
- **校验的表**:[[tbl_reconciliation_t_settlement_template]]、[[tbl_reconciliation_t_settlement_detail]](= `related_tables`)
- **相关日志**:待补
- **所属流程**:[[flow_manual_fund_settlement]]

## 前置条件
- 已创建并审核通过的结算模板(`settlementType` + `biz_product_code` + 出款账户配置正确)。
- CMA 账户间互转模板已配置 `settlement_code`(如 `CMA3->CMA4`)。

## settlementType 与 biz_product_code 映射

### INNER_ACCOUNT(内部账户出款)
| biz_product_code | 适用场景 |
| --- | --- |
| `500105` | 出备付金体系的内部账户出款;FAB 0040 AED / FAB 0062 USD 出款(目标为本行或他行 IBAN,FAB219/FAB220/FAB223) |
| `500108` | 不出备付金体系的内部账户出款(payby 内部资金调拨);FAB 0040 AED → ENBD CMA、FAB 0062 USD → ENBD CMA |
| `500109` | ENBD CMA3 AED → FAB 0040 AED(ENBD210) |
| `500110` | ENBD CMA3 AED → ENBD CMA2 / CMA4 AED(ENBD209) |
| `500111` | ENBD CMA2 AED → ENBD CMA3 AED(ENBD204) |
| `500113` | ENBD CMA4 AED → ENBD CMA3 AED(ENBD201) |

### MERCHANT_ACCOUNT(商户出款)
| biz_product_code | 适用场景 |
| --- | --- |
| `230601` | AED to AED |
| `230602` | AED to USD |
| `CB001` | CA 向 CA 内部账户转账(FTS) |
| `CB103` | CA 向 CA 以外账户转账(FTS) |

## 操作步骤
1. 选定对应 `biz_product_code` 的模板,发起结算申请并审核通过。
2. 等待系统调拨完成,确认 Settlement Result。
3. 查账务流水,核对 DR/CR 分录。

## DB 校验点 / 预期资金流(DR/CR 分录)

### FAB 0040 / 0042 AED 出款
两段式登账,经"待清算应付"科目过渡:
| 步骤 | DR | CR |
| --- | --- | --- |
| 1 | 78429990020010001 | 78429990030010002 |
| 2 | 78429990030010002 | 78430030020010002 |

### FAB 0062 USD 出款(H2H)
先冲减备付金,再过渡到待清算出款科目:
| 步骤 | DR | CR |
| --- | --- | --- |
| 1 | 84040030020010001(USD capital reserve-FAB-0062) | 84029990030010002(Other Accounts Payable - Pending check for settlement - 0062 USD) |
| 2 | 84029990030010002(Other Accounts Payable - Pending check for settlement - 0062 USD) | 84040010010010001(FundOut Pending for Clearing-FAB-H2H-0062 USD) |

### ENBD CMA 账户互转(按 settlement_code 区分方向)
| 产品码/方向 | DR | CR |
| --- | --- | --- |
| 500111(CMA2→CMA3) | 78430010210010003(FundIn Pending for Clearing-ENBD CMA3) | 78430030040020001(FundOut Pending for Clearing-CMA2-ENBD204) |
| 500113(CMA4→CMA3) | 78430010210010003(FundIn Pending for Clearing-ENBD CMA3) | 78430030040040001(FundOut Pending for Clearing-CMA2-ENBD201) |
| 500110(CMA3→CMA2) | 78430010210010002(FundIn Pending for Clearing-ENBD CMA2) | 78430030040030001(FundOut Pending for Clearing-CMA3-ENBD209) |
| 500110(CMA3→CMA4) | 78430010210010004(FundIn Pending for Clearing-ENBD CMA4) | 78430030040030001(FundOut Pending for Clearing-CMA3-ENBD210) |

> 注:500110 在 CMA3→CMA2 与 CMA3→CMA4 两个方向下 CR 科目相同(78430030040030001),方向由模板 `settlement_code` 控制。

## 预期结果
- `t_settlement_detail` 中 Settlement Result=SUCCESS,Result Code/Msg 无报错。
- 实际登账的 DR/CR 科目与上表对应 `biz_product_code` / 方向一致。
- 失败场景:Settlement Result=FAIL,Result Code/Msg 回填(如 `FTD-06...`),无错误登账。
> 不确定 / 缺失的点(物理列名、日志关键字)标「待补」,留待人工补充。
