---
title: Wallet Redesign Send Money 用例图
domain: fund-out-transfer
kind: wiki_page
slug: wallet-redesign-send-money-usecase
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:ad8e760d-e16c-4812-8f5d-a82c3e45fcdc
tags: []
---

# Wallet Redesign Send Money 用例图

本页以 UML 用例图描述 Wallet Redesign 中 Send Money 功能涉及的参与者、用例及其 Include/Extend 关系，业务域为 `fund-out-transfer`。

## 参与者

- **Payer**：发起转账的一方。
- **Payee**：收款方，需完成 KYC 才能收款。

## 系统边界与用例

用例划分到三个 package：

### transfer

- **Send**：由 Payer 发起。
- **Refund**：含 extension points，作为 Send 的扩展用例。
- **Receive**：含 extension points，作为 Send 的扩展用例。
- **Transaction Detail**：Payer 与 Payee 均可查看。

### Botim

- **Notification**：被 Send 与 Receive include。

### kyc

- **Kyc Finished**：与 Payee 关联，被 Receive include。

## 关系汇总

### Include 关系

- `Send` —«Include»→ `Notification`
- `Receive` —«Include»→ `Notification`
- `Receive` —«Include»→ `Kyc Finished`

### Extend 关系

- `Refund` —«Extend» `Send`，扩展点：**Expired**（交易过期时触发退款）
- `Receive` —«Extend» `Send`，扩展点：**Payee KYCed**（Payee 完成 KYC 后触发收款）

### Actor 关联

- Payer → Send、Transaction Detail
- Payee → Kyc Finished、Transaction Detail
