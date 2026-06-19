---
title: ChargeBack Case状态管理
domain: risk-control
kind: wiki_page
slug: chargeback-case-status
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/1333395487
tags: []
---

# ChargeBack Case状态管理

本页说明 ChargeBack 记录的 Case 状态枚举及其与 code 的映射，以及 New case 与历史记录在后续处理（CasePool 同步、邮件、冻结）上的差异判定规则。

## 状态枚举与映射

下表列出 case status 与映射 code、描述：

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

- 最常用状态：**New case (NC)**。
- 注意 `FULFILLED` 与 `IN_CYCLE` 同映射为 `IC`；`CHBK_ACCEPTED_BY_MERCHANT`、`NO_RESPONSE_BY_MERCHANT` 与 `LOST` 同映射为 `LOST`。

## New case 与历史记录的处理差异

状态决定记录后续触发哪些下游动作：

- **New case 记录**：
  - 同步到 CasePool（参见 [[chargeback-casepool-sync]]）
  - 发送邮件（参见 [[chargeback-mail-notification]]）
  - 触发冻结（参见 [[chargeback-freeze-logic]]）
- **非 New case 记录（仅限历史记录）**：
  - 仅同步到 CasePool
  - **不发送邮件**
  - **不触发冻结**

## history flag 判定

- 历史记录依据上传 Excel 中的 `history flag` 字段判断：**字段有值即视为历史记录**。
- 历史记录无论其 case status 是什么，都按"非 New case"路径处理（只走 CasePool 同步）。

## 相关页面

- 整体业务背景：[[chargeback-business-overview]]
- 端到端处理流程：[[chargeback-process-flow]] / [[flow_chargeback_processing]]
