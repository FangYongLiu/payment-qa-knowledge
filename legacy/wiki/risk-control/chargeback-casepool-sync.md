---
title: ChargeBack CasePool同步逻辑
domain: risk-control
kind: wiki_page
slug: chargeback-casepool-sync
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:b45ef58e-e6ac-4d48-9837-7307c6d42c4e
tags: []
---

# ChargeBack CasePool同步逻辑

ChargeBack 文件解析后新增的记录会同步到 CasePool，本页说明同步过程中 `CaseType`、`Case Source`、`Memo` 三个属性的取值规则。

## 同步范围

- New case 记录：同步到 CasePool，并触发邮件与冻结（见 [[chargeback-mail-notification]]、[[chargeback-freeze-logic]]）。
- 非 New case 的历史记录（Excel 中 `history flag` 有值）：仅同步到 CasePool，不发邮件、不冻结。
- Case 状态枚举与判定见 [[chargeback-case-status]]。

## 属性映射规则

同步到 CasePool 的 ChargeBack 记录按以下规则填充属性：

### CaseType

- 固定值：`Chargeback`

### Case Source

- 取值：`Acquirer`，对应当前上传文件的收单行
- 可选值：`VISA` / `MASTERCARD` / `MAGNATI` / `ADCB` / `CKO-HISTORY`

### Memo

按 Acquirer 区分拼接规则：

- Acquirer 为 **VISA / MASTERCARD**：
  - `Acquirer + aml.t_chargeback_pool.id + aml.t_chargeback_pool.caseNo`
- Acquirer 为 **MAGNATI / ADCB / CKO-HISTORY**：
  - `Acquirer + aml.t_chargeback_pool.id`

## 相关链接

- 业务总览与整体流程：[[chargeback-business-overview]]、[[flow_chargeback_processing]]
- 同步后续动作：[[chargeback-freeze-logic]]、[[chargeback-mail-notification]]
