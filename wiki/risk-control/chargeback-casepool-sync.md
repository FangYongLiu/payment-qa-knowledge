---
title: ChargeBack CasePool同步规则
domain: risk-control
kind: wiki_page
slug: chargeback-casepool-sync
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/1333395487
tags: []
---

# ChargeBack CasePool同步规则

ChargeBack记录新增后会同步到CasePool，本页说明同步时CaseType、Case Source及Memo的字段拼接约定。

## 同步字段约定

| 字段 | 取值 |
|---|---|
| CaseType | `Chargeback` |
| Case Source | `Acquirer`（取值范围：VISA / MASTERCARD / MAGNATI / ADCB / CKO-HISTORY） |
| Memo | 按 Acquirer 区分拼接规则（见下） |

## Memo 拼接规则

按收单行（Acquirer）不同，Memo 的拼接方式不同：

- **VISA / MASTERCARD**
  - 格式：`Acquirer + aml.t_chargeback_pool.id + aml.t_chargeback_pool.caseNo`
- **MAGNATI / ADCB / CKO-HISTORY**
  - 格式：`Acquirer + aml.t_chargeback_pool.id`

## 同步范围说明

- 所有新增的 ChargeBack 记录均会同步到 CasePool。
- **New case** 记录：同步到 CasePool，并触发邮件发送和冻结。
- **非 New case 记录（仅限历史记录，按 Excel 中 `history flag` 字段判定）**：仅同步到 CasePool，不发送邮件、不触发冻结。

## 相关链接

- [[chargeback-case-status]]：Case状态枚举与映射，决定是否走完整同步流程
- [[chargeback-freeze-logic]]：New case 同步后触发的资金冻结逻辑
- [[chargeback-mail-notification]]：同步链路中的邮件发送判断
- [[chargeback-process-flow]]：完整处理流程上下文
- [[chargeback-business-overview]]：ChargeBack 业务总览
