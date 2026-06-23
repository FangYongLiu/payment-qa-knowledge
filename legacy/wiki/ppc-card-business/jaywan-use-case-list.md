---
title: Jaywan预付卡用例清单
domain: ppc-card-business
kind: wiki_page
slug: jaywan-use-case-list
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:b4ddb781-c8c9-4531-9714-54f78aa19fea
tags: []
---

# Jaywan预付卡用例清单

本页按优先级列出 Jaywan 预付卡涉及的 Vendor API（Dgpay 调用方向）与 Institution API（Dgpay 回调方向）用例清单，作为 [[jaywan-phase1-system-design]] 与 [[jaywan-phase2-system-design]] 的需求输入。完整产品背景见 [[jaywan-prepaid-card-overview]]，端到端业务流程见 [[flow_jaywan_card_lifecycle]]。

## 优先级说明

- `0`：基础与虚拟卡核心能力，Phase 1 必需
- `1`：实体卡能力 + 交易通道（Phase 1）
- `2`：交易类与 Institution API 主链路（Phase 1）
- `3`：异常恢复、状态联动、通知等增强项

## Vendor API 用例（调用 Dgpay 方向）

| 用例 | Vendor API | 优先级 |
| --- | --- | --- |
| Common API Invoking - GetToken | `GetToken` | 0 |
| Create Virtual Card | `CreatePrepaidDigitalCard`（错误恢复：`GetPrepaidCards`） | 0 |
| View Card Detail | `GetPrepaidCardInfo` | 0 |
| Lock / Unlock Card、Replace Card、Close Card | `UpdatePrepaidCardStatus` | 0 |
| Reset PIN | `PrepaidCardPinOperation` | 0 |
| Apply Physical Card | `CreatePrepaidEmbossData` | 1 |
| Activate Physical Card | `ActivatePrepaidCard` | 1 |
| Auto sync mobile change | `UpdateMobilePhoneNumber` | 1 |

## Institution API 用例（Dgpay 回调方向）

| 用例 | Institution API | 优先级 |
| --- | --- | --- |
| Institution Get Token | `get-token` | 2 |
| Transaction | `provision` | 2 |
| Transaction Reversal | `reversal` | 2 |
| Balance Inquiry | `balance-inquiry` | 2 |
| Declined Transaction | `declined-transaction` | 3 |
| Update Card Status from Bank Portal | `update-prepaid-card-status` | 3 |
| Delivery Tracking | `notify-courier-process` | 3 |

## 相关说明

- Replace Card：Dgpay 暂无虚拟卡 replace API，需先 `UpdatePrepaidCardStatus` 关卡再 `CreatePrepaidDigitalCard` 重新开卡（详见 [[jaywan-vendor-qa]]）。
- Apply Virtual Card 错误恢复：当 `CreatePrepaidDigitalCard` 超时不可知时，使用 `GetPrepaidCards` 对账并补登或关卡。
- Phase 1 Scope 覆盖优先级 0/1/2 用例；清结算相关用例见 [[jaywan-clearing-settlement-design]]；Phase 2 增量（Replace/Close/ChargeFee/Manual Release/Pending Transaction Chasing）见 [[jaywan-phase2-system-design]]。
- 用例对应的产品规则与字段约定见 [[jaywan-product-qa]]。
