---
title: ChargeBack Case状态管理
domain: risk-control
kind: wiki_page
slug: chargeback-case-status
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:b45ef58e-e6ac-4d48-9837-7307c6d42c4e
tags: []
---

# ChargeBack Case状态管理

本页说明 ChargeBack 记录的 Case 状态枚举、状态码映射，以及不同状态对 CasePool 同步、邮件发送和资金冻结行为的影响。

## 常用状态

- 最常见的状态是 **New case (NC)**，对应新增的 ChargeBack 记录。

## 状态枚举与映射

下表列出 Case Status、对应 code 与描述：

| case status | code | desc |
|---|---|---|
| WON | WON | WON |
| ARBITRATION_LOST | ALOST | ARBITRATION LOST |
| ARBITRATION_RAISED | AR | ARBITRATION RAISED |
| LOST | LOST | LOST |
| IN_CYCLE | IC | IN CYCLE |
| FULFILLED | IC | FULFILLED |
| CHBK_ACCEPTED_BY_MERCHANT | LOST | CHBK ACCEPTED BY MERCHANT |
| NO_RESPONSE_BY_MERCHANT | LOST | NO RESPONSE BY MERCHANT |
| NEW_CASES | NC | NEW CASES |

注意：`FULFILLED` 与 `IN_CYCLE` 共用 code `IC`；`CHBK_ACCEPTED_BY_MERCHANT`、`NO_RESPONSE_BY_MERCHANT` 与 `LOST` 共用 code `LOST`。

## 状态对下游处理的影响

不同状态触发的下游动作不同：

- **New case 记录**：
  - 同步到 CasePool（详见 [[chargeback-casepool-sync]]）
  - 发送邮件（详见 [[chargeback-mail-notification]]）
  - 触发资金冻结（详见 [[chargeback-freeze-logic]]）
- **非 New case 记录（仅限历史记录）**：
  - 仅同步到 CasePool
  - **不发送邮件**
  - **不触发冻结**

## 历史记录判定

- 根据 Excel 文件中的 `history flag` 字段判断：**有值即为历史记录**。
- 历史记录即使状态非 New case，也会进入 CasePool，但跳过邮件与冻结逻辑。

## 关联页面

- 业务总览：[[chargeback-business-overview]]
- 端到端处理流程：[[flow_chargeback_processing]]
