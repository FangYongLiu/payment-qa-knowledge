---
title: Jaywan Phase2系统设计任务
domain: ppc-card-business
kind: wiki_page
slug: jaywan-phase2-system-design
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:b4ddb781-c8c9-4531-9714-54f78aa19fea
tags: []
---

# Jaywan Phase2系统设计任务

本页汇总 Jaywan 预付卡 Phase2 阶段的系统设计任务，覆盖替换卡、关闭卡、人工释放、ChargeFee 以及 Pending Transaction Chasing 五项功能。Phase1 与清算结算相关任务请见 [[jaywan-phase1-system-design]] 和 [[jaywan-clearing-settlement-design]]。

## 范围概览

Phase2 任务列表：

| Case | Dgpay API | Brief | Workload | Developer |
|---|---|---|---|---|
| Replace Card | UpdatePrepaidCardStatus / CreatePrepaidDigitalCard | CGS API | 1d | yu.tang |
| Close Card | UpdatePrepaidCardStatus | CGS API；Close member check | 1d? | yu.tang |
| Manual Release | - | 人工释放长时间未 post 的 dual message | - | - |
| ChargeFee | Institution API | 实现 ChargeFee 与 ChargeFeeCancel | - | - |
| Pending Transaction Chasing | Internal Mechanism | 内部机制 | - | - |

相关用例清单见 [[jaywan-use-case-list]]，端到端流程见 [[flow_jaywan_card_lifecycle]]。

## Replace Card（替换卡）

- 涉及 Dgpay API：`UpdatePrepaidCardStatus` + `CreatePrepaidDigitalCard`
- 设计文档：CGS API（无独立 SD 链接）
- 工作量：1d
- 关键说明（来源 [[jaywan-vendor-qa]] / [[jaywan-product-qa]]）：
  - Dgpay 当前没有 replace virtual card 的独立 API。
  - 替换流程 = 先调用 close（`UpdatePrepaidCardStatus`）→ 再调用 apply（`CreatePrepaidDigitalCard`）。
  - 该流程与 `ReplaceCard` 物理卡替换流程等价；Dgpay 的 `ReplaceCard` 方法以 emboss 信息作为输入，正常仅用于物理卡。
  - 不能直接移除 replace card 功能，需通过 close + apply 组合实现，或等待 Dgpay 新的 replace API。

## Close Card（关闭卡）

- 涉及 Dgpay API：`UpdatePrepaidCardStatus`
- 设计文档：gppc-SD-Jaywan Virtual Card（CGS API）
- 工作量：1d?
- 关键点：需要做 Close member check（关户成员校验）。

## Manual Release（人工释放）

- 范围：对长时间未 post 的 dual message 交易进行人工释放。
- 无 Dgpay API 直接对应（属于内部运营动作）。
- 与交易侧 PROVISION / REVERSAL 流程相关，参见 [[jaywan-clearing-settlement-design]]。

## ChargeFee

- 设计文档：gppc-SD-Jaywan Transaction
- 接口归属：Institution API（即 Dgpay 调用 Institution）
- 实现内容：
  - `ChargeFee`
  - `ChargeFeeCancel`

## Pending Transaction Chasing

- 类型：Internal Mechanism（内部机制，非 Dgpay API）
- 用途：追踪 / 催促处于 pending 状态的交易，使其最终落到正确的终态。

## 相关参考

- 产品侧问题（如 Replace Card 是否可只删除等讨论）：[[jaywan-product-qa]]
- 厂商侧问题（Dgpay 对 Replace 流程的回复）：[[jaywan-vendor-qa]]
- 产品总览：[[jaywan-prepaid-card-overview]]

</br>

> 注：上表中部分 Workload / Developer 字段在原文中未填，以 `-` 标识。
